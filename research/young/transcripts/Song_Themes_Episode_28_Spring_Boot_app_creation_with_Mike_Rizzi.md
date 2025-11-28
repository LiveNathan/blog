# ＂Song Themes＂ Episode 28： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=XEppm1QR8ew

---

## Transcript

all right hello folks folks welcome to episode 28 pairing stream uh where Mike and I are working on uh his song themes
app welcome everyone how's it going Mike doing well doing well so I will give you and the viewers a heads up that I
might be taking a lot today so um where did we leave off last time I remember we had a failing test test yeah you want
to jump right into the code sure did you want to refund anything beforehand um I don't think so so we're working on High
level requiring the heter rows to have specific columns and then we're currently handling here on J 81 handle multiple
themes oh I was looking through through jira um and just looking back at some of the earlier stuff uh uh jur 60 we
actually did the other day which was uh split the result class into two concrete right check that dopamine yes anything
else we missed that we uh nothing that was that was obvious okay cool um well 42 but that was on you installing the the
the tab shifter uh plug oh right yeah 42 yeah so so last time um we uh fixed some failure messages and so uh finally
split the the result class and I think we're much happier with with the result classes more we can do um and we'll
probably see sort of see some of the awkwardness there um but I think uh uh I think I think it'll be okay hey s yeah we
can just in time it as the awkwardness becames annoying we can tackle it yeah and we can decide how much we want to do
um so today I gave 5050 odds for whether we' get to persisting to the database so we'll see we'll see what happens so
place your bits okay I guess we need to create a betting app now yes let's let's go and do that he cha let's Yak shave
this yes nine levels deep so um did we run the test I didn't see I did uh okay I see failure is Right which is in the
tsv song parser test I think it's did it fail because we're still starting it or let's see failure and missing a theme
same one oh right because we're not we're not right because we're not checking uh checking that stuff so this is this is
proper tdd we we've got behavior that we'd like in terms of failures um and so we need to to go and Implement that oh uh
if you go back to the result class um uh we had something commented out for for permits uh and there's some weirdness
with with how permits works and sealed in permits um there might be a better way to to do this but I have to do some
more experimenting uh so we can probably just delete that comment for now do we want to add the the research to our jira
um no because that's that's something that that I'm just going to do okay because there's some interesting stuff you can
do with interfaces and sealed and and I'm not sure if it's a if it's the right fit for for what we need um but uh I I
did some playing around because I was like why is why isn't that isn't that working um do you want to combine seven and
eight yes I don't know how it got like that that's weird uh because we added the the comment that's why I got clean yeah
I'm actually pretty happy with with where the result is right now uh one thing we could do although because we have our
custom result assert it's not as necessary but a lot of the implementations I was looking at for result they Implement
both is success and is failure um which I guess kind of makes sense it kind of makes it easier even though one is the
opposite of the other it means you would never need to uh you know put a bang in front of it in some kind of if
statement so in other words pushing it down to the concrete classes as a yeah and basically let them do the inversion to
to make it easy on clients to to not have to call one or the other like basically our current case which is uh we're
expecting that it uh that it fails um we we get around that because we're using our custom assert and so that that makes
it easier but um I know there's at the string level we have a couple of uh we weren't we didn't generif our our result
string so that one we're doing directly so maybe if we see it again we'll probably implement it is is what I say Okay um
let me just answer a couple of questions so trap asks what's the testing dependency that you're using to test with so we
use um we're using junit for the standard test Runner uh but for our assertions the assertion Library we're using is a
shj uh so search J is is a very popular Library um spring uses it I've been using it I contributed to it way back when
so highly recommend it so search a uh you actually go to search j.com they they actually lost some time back so if you
look at um if you look at the import Imports uh oh and we don't even see it here because we're using our custom one why
don't you switch to a different test yeah yeah so we're so aarch a.org they lost that domain um really yeah so uh uh so
I actually bought aarch a.com which redirects you to the right place but they lost they lost that which is unfortunate
oh wow uh and swegi asks um yes we did that last time you missed it last I guess you missed it uh we split the result
into two inner sub sort of inner sub classes nicer and hey there Doo to attitude also cook all right all right uh so
let's let's go back let's go to our failing test just doing and so we're basically saying since this doesn't have theme
as a required we need to fail so yeah so let's go look at our our implementation of parong and so we can see where we
have the extract themes we're not doing so let's um oh yeah I remember this was this was not straightforward right
thankful enough welcome uh so what's the simplest thing we can do um I think we had come up with the idea of checking
for the required no we were validating the the column matching first uh and then we go so right so we pulled that out
because that was that was previously inside an extract column and that made no sense um so I think extract themes we've
got to well let's go back and and look at again right so because uh on line 67 we're doing a filter we're actually
throwing away our our is uh any failures to extract the the theme um and because it's a stream we can't like go through
it multiple times to there's this is where you you can sort of get more functional um and you can sort of collect uh and
I think we've done done this a bit before we could sort of map it to I feel like we've had this this it's funny is like
I feel like we've had this this discussion of of how we were going to do it and I don't remember what the result was
yeah I remember we did too so we could we could map um so Group by the the failure and and and the not failure uh but I
think that's that's too hard uh complicated um I say we do the simplest thing that could possibly work even if it's ugly
just to get this test to pass which would repeat the extract column for the first for for theme one because if theme one
is there right so let's let's be clear about our expectations so if theme one is there that's that then we're okay right
so if theme one's not there then it's a definite failure right and and we I think we decided that if theme two is there
but theme one is not there that that's not good right that the minimum was theme one right so let's let's let's
Implement that that requirement so let's 65 so if we get the stream how do we do it without ex consuming the stream can
we just well we're creating the stream on 66 we have this this we know exactly what're we're just going to check theme
one directly ah okay so we could just do like call colum mapper do extract yeah column and still use columns yeah comma
now we're just doing it for list of theme one uh well it's not a list of it is literally just theme one so just theme
one yeah and then we what is that going to be result of string yeah can we use result here I guess we can do so right
now here's where where we'd love to have is failure right uh so how about we just Implement that just just right now
let's put this on hold okay as in that way yeah that's that's fine uh and let's go to result and just just implement it
without test driving it first I don't think we need to test drive this okay we're we're basically test driving is it is
do we have an is failure method that returns Boolean that Returns the correct thing and I think we can right use our
professional judgment yeah so we're gonna do this within not the abstract base class but in the uh we want to do it in
the abstract based class um do yes uh but I think we have all the methods at the bottom which I think we should bring to
the top those abstract Methods at the bottom okay I don't remember why we put them at the bottom there was some
rationale at the time but I forgot what it was uh I think we should put them below the Statics but above the um the
actual implementations I thought we' actually moved it but I guess we didn't so you want to put it like 24 okay so after
the stat creation methods but before the implementations yeah got it okay um and now let's let's add an is failure
method and this we could actually just Implement at the base class because it's just going to be the opposite of of is
Success oh right it's not goingon to be different for for one of the failure uh we got to write that in the that yeah
full that that that would be the the grouping by collector if we decided to do that but I don't think that yeah so um uh
now that we have that method I'm pretty sure that that we can eyeball that and be confident that it works um and we'll
sort of indirectly be testing that do we return we're doing a return yeah so so we're gonna have to um convert extract
themes to return a result of a list of strings I I wonder if we should to avoid having to make those changes now take
the code we just wrote collar this part yeah yeah half you want to do a guard Clause there really oh we got result well
it's not going to be it's not going to be a a guard Clause it's going to be a choice so we're going to do if it's a
failure we're going to do one thing um so in fact actually oh we're only going success right oh uh but for now we'll
we'll basically uh no let Let's do let's do is failure and then just do a return even though that's not fully what we
want our song returns a result object it's not going to be happy so we'll have failure uh yes we will have to to so
basically what we have online I don't know 60-ish yeah so something like what we 66 oh but we haven't started collecting
them but we will use well we're just GNA it oh actually result and what did I do wrong result dot that should be do
failure be theme one result dot failure messages right so this is ugly um but it should get us to to Green yeah yeah
let's find out and we could probably flip 42 as well once we get pass yeah yeah yeah we got to pass uh so let's oh I got
this to pass yeah okay now we refractor um so let's fix 42 since we now have his that and when you say swap meaning yeah
like that what you did yes okay Flip Flip Flip I guess right uh so let's run our Point yeah because at that point there'
s no use trying to extract columns the other columns because it's a dead row it's a dead song row because we're paring a
single song here right right which means we can't do anything so it's it's okay that we're doing it before we do right
we don't need to collect failure messages here because failures is that right I think so so let's um I think we can
ratch it up our yes I'm gon yeah minute uh so swegi mentions we could try something like map uh take while yeah the
thing is if we do that we lose the failure messages that come from the extract column so extract column does its own
validation uh and so if we do the mapping actually because if we're only taking while it's success I don't know that
that doesn't feel as clean and I think there's there's some other stuff we could that the result class could be a bit
more so they result class implementations that that do a lot more about handling this kind of thing with with
combinations um where you basically can stream through all of the results and combine them uh so you map them you would
map the extract column you get out of that a result and then you could combine all the results and what you'd end up
with is if any result combines with failure all you get out is just a failure uh so that might be something we we try
yeah we were we were just trying to get get get to Green uh asks if we had to start from scratch would we out for a
custom CSV writer so first of all we're not doing CSV we're doing tsv um second of all uh if we use the library we would
still have to do this kind of validation because the stuff we're dealing with here is about what's required in our data
what columns do we require which ones are optional uh and maybe a library has that functionality but there's also um
even though we may not Implement that anytime soon uh there's also a dependent column like if you have uh release type
you must have the other one release title or the other way around anyway there's a dependent column where it's like if
you have one you have to have this other one um so I don't know if any libraries do a good job of that um but I don't
know maybe or maybe we take our library and gener and generalize it I mean it's really interesting because like the
actual parsing is Trivial it's one line of code like parsing and separating the columns it's all the rest of the stuff
of dealing with validation uh that's actually what we're dealing with so I don't I don't I don't know if anybody wants
to do some research on the available tsv parsers and see if they offer that kind of stuff um I I suspect there are some
that probably do have but who knows all right um I'm going to rerun the test just to make cool so are we going to
ratchet this up uh or is this failure good enough do we need to I'd like to see the message because one of the things
that I that um uh we'll want to missing like song title and it's missing theme one that we get get both of those do we
do a um contains exactly uh what's our options from this point it doesn't affect we have much messages is that not clear
should we call that failure because what it returns is failure messages right yeah I'm with you I think we that and we
could do a renum on values if we feel that that's unclear and call yeah and that's the one we'll eventually have to
generif maybe okay um uh let's go back to our our test um let's do just a a commit of of the rename um what do you think
result some res properties uh specific I mean it's like they could check by looking at the diff I just say did a great
yep all right so now we know it's failure messages yes so now we do failure messages and then we can go exactly and then
we do a characterization test yeah I think here we can do a characterization so we expect the only failur is about the
missing theme ones that's that's what we to well the other columns were fine but even if they were wrong it wouldn't
yeah yep you could do the diff if you want but you either way yeah and then if we do this paste will it do the Escape
correctly it should uh unless you didn't copy the right thing oh oh the green was showing the difference not yeah it's
green not yeah yeah yeah yeah yeah yeah yeah and so it escaped it correctly y so now it should pass now it should yes
cool all right so I think we can just commit that and say message um so now I think we want to look at uh do we combine
multiple failure messages for for multiple missing required coms I that be if you open up the nested par so we've got
two failure messages when missing two required columns we could modify that one to basically make it uh multiple failure
messages when missing multiple required columns the bottom one or yeah the bottom one because that's oh but then we'd be
well I guess we could be passing in nothing um well we can pass in a column that's not a required column right so let's
yeah let's do that let's rename it to just say um multiple and keep it two or make it well it's going to be more than
missing two just required columns missing all required columns because right now there's three uh sure then uh don't
forget don't forget to hit enter yeah okay oh man hit enter the wrong way okay multiple by the way for tests I know it's
I know it's a habit you may not want to yeah you don't need to do the you don't need to do the the the rename yeah yeah
it's a habit fail messages thing all requir columns yeah and then one column that's not required as notes right you can
say no notes ah sure um or I could just say something by so now this should fail because when yeah let's change uh Line
220 to be three but we'll leave the rest as a characterization test right well this what's really this will probably
fail right but not just characterization test it's going to probably just say missing theme one column and that's it how
about we comment out this this thing so we can see exactly what what we get is not what we want so we expect this to
fail because uh we're only gonna sorry comment outline 220 to 20 ah okay got it so we expect oh I know what you're
saying yeah yeah yeah we expect it to return a single message having to do with Miss the missing theme theme because it
never even made it to the artist in song Tit better right right so we got missing required Comm theme one and we're
missing the artist and song title ones which is which is what exactly what we expected so that's good our code uh does
exactly what we thought it did expected y now is it what we want it to do uh yeah it's not what we wanted to do yeah so
let's um so do we want it to actually have yeah I think we should add that now now we add this yeah be careful about
your double quotes I think I'll do it let's see if I can do it this way and get it right H but you pasted one too many
that's why I'm saying be careful thought it was a Oh from down below I the copy there we go now the we could change our
messages to make our lives easier and not and just use single quotes oh but now is probably not the time to it shift
control shift o uh alt control L talking about reat yeah there we go that's better yeah okay so now it's gonna fail
again right and now it's gonna fail because it found the theme one but didn't find the artist and song title right y yep
okay all right so let's make it work see so we've got should we put the has size back in or wait till we get this
working first um wait we can we can put I mean we might even delete it I'm not anymore but I kind of like it to make it
clear that it's three I mean it's I mean you could mentally parse this and go yeah that's three entries I think we
should leave it commented out we can then add it back yeah okay so as far as making it work so now we need to accumulate
the failures not do a fail and bail here um so that's not the failure that's not the failure we need to worry about oh
um I think we can just move this to uh basically to 57 let me see what 57 is after the extract themes so 57 is basically
we want to say if they've if if they're all all the ones that we care about are successful so we would need to add in
our theme one result theme one result right um yeah the second item yep and then for the failure message though will
that then we can success is fine then we can just dupe dupe 65 and pull it from see yeah what I like about this what you
just did um is I was mentally going how can we move this code down right whereas you stepped back and went well what do
we need the code down here to do rather than my mental model of trying to keep this that we just wrote that was is
working right yeah now we can delete that that exactly y yeah I'm just noticing my own mental Behavior yeah yeah and
where they went so now this should work it should work yeah uh some tests might fail if if there were but I guess not I
was just thinking we added a basically a Boolean to to 54 that could have affected other ones but um but it was since it
was testing for Success then then that surprising that's a good place for that so this is ugly um method uh but it works
if you want to put the the has size of three back you can and then we'll commit okay uh so do to attitude mentions uh
when pairing I do Navigator wins all decisions until driver calls a huddle um when pairing I tend not to be that strict
I tend to be much more um fluid much more active as as as a driver uh because it's only two of you uh in an ensemble um
that's different uh then you then because otherwise you can get into a multi-way discussion uh when it really should be
the nav Navigator wins which is interesting was in the at the um software teaming conference last week Woody was saying
the opposite that it's that once the team gets mature enough it's okay to to have those mway discussions yes yes that
that's absolutely true that uh once teams do get used to ensembling and you are no longer worried about um somebody
dominating the conversation then then you then you can start okay um so yeah I don't know if I'd use the word over
engineering swegi it's it's more like too many too too too much just too much goes yeah that's big method so uh commit
message we now accumulate yeah all messages yeah for all all missing column failure messages all missing required column
failure messages and I'm gonna take another break once I hit good because there was a a question that I wanted to
address so oh cool I'll keep my head sound so I can listen but turn off right uh so tkes hey tkes um uh I think of post
layoffs period mid 20 2024 in general um our industry will not be the same uh I think we've got two two problems uh from
an employee standpoint which is one is um companies decided they wanted more profit um generally large public companies
uh but also uh so large public companies want more profit because they want their stock price to go up uh regardless of
whether firing people and laying people off is a good thing or not it is perceived by uh investors as being a good thing
um secondly uh startups because we are no longer in a zero interest rate policy environment and will likely not be in
one for for the fores seable future um money is no longer free which means they actually have to make money and so
startups will have also and will continue to uh fire people uh because they hired too much um and they can't effectively
use use those people uh so we're still seeing that um the number of layoffs sort of if you look at how many layoffs now
you know in the past month or so versus a year ago it's less um but we're still seeing it uh there are other companies
in the world other than tech companies and startups so those are still hiring uh but there're now a lot more people
looking looking for jobs um I don't think it's any different for Java devs than anything else in fact it might even be
better than for Java devs because startups generally don't use Java uh right or wrong uh they generally don't use don't
use Java and so they weren't hiring them anyway um and the companies that do use Java tend to be the larger older more
stable companies especially Financial firms and they've generally uh done pretty well whether or not you want to work
for them is a separate issue um then there's AI which at least people think that that means they don't need uh
developers but all so sort of speaking of Legacy code um uh AI is going to be great for generating Legacy code right off
the bat because it's terrible uh terrible terrible terrible I mean I it's just so awful I there's there I was talking
with somebody about um yeah anyway I'm not I'm not going to go on on that rant because we've been there before but
basically there is a perception that um AI can replace developers uh true or not perception is what matters um not
reality and so therefore uh companies are thinking they can get away don't I think it's going to be if we're lucky the
latter part of this year but probably won't be until beginning of next year uh before things start to to sort of get
back on on the upswing is is sort of my my completely gut-based intuition uh uh prediction and we all work oh gold PL in
the result class well we're probably going to do something to to add to the result class uh yeah can definitely over it'
s I mean this is why we didn't adopt an existing result class is because it's some of the out sort of ones that I've
seen um they do a lot and it's not it's a lot of code that I don't even necessarily fully understand what it's trying to
do um and so I'm uncomfortable taking on that code uh not to mention that taking on a a library dependency for just
what's basically one or you know a couple of classes in one file feels um oh oh and there was another question uh ful
asks about JQ assistant uh ensuring the rules of hexagonal architecture um that's what we use ARC unit for um uh Arc
unit which just came out with 1.3 um makes that possible I haven't used JQ assistant directly uh I'm not sure what what
benefits it would have Arc units API is interesting um not obvious and the documentation could could be better but it
does pretty much everything that that I want uh we don't have it in this project yet um because we don't have that many
layers uh we don't once we add the the database we'll probably want it yeah we'll probably want to do that after uh so
are we I think we we're not done because I think we we should be doing some refactoring here yeah for song parser going
back to song parser yep the one that made um sui uh I don't know if quiver is the right word but oh I think sui was
talking about the result class not oh I see not the Parton well it certainly make my Spidey Sense go this thing is huge
well okay I mean if nothing else I don't even think it can fit on the screen anymore I know look unless you completely
maximize it and then it just barely fits so it's maybe I mean a lot of this you can't extrac into methods particularly
well it's kind of passing a lot though so I think I think the the the problem with our way to combine them because what
we'd like and and you sort of uh mentioned an aspect of it if everything works what we what we might like is a map of
column names to values because then it would in fact then we might even be able to just hand that into song and let it
figure it out um if not then it's pretty easy to pull it out one by one which is what we're kind of doing on on line 56
55 through 58 right um but that's if we get all success if we get any failures we'd like to basically what we want to do
and this is why other result classes have this idea of a combine um where you just take any two results and you combine
them and what you get out is if one of them is a failure the result is a failure the the outome of the combination is a
failure if they're both successes then you get the combination of them uh but we don't have a good way to combine
successes either because we just have this result so um so if you go back to the song parser right so like line 46 what
we get out of that is a result of string and by itself that's not enough information if we wanted to to later create
yeah we don't know it's artist we just know exactly exactly of Str yeah yeah um oh hey dudan uh yeah so it's not just
architecture stuff so I actually wrote specific constraint check that makes sure that only for example uh the repository
class can call a specific method on a domain object for reconstituting it because as we'll see if we get to to database
stuff we're going to have to pull stuff from a database and reconstitute the object but the only and that so that needs
to be some kind of Constructor or maybe it's a static Factory method um so it has to be accessible from the repository
but they're in two separate packages so therefore it has to be public except you don't want that method that
reconstitute method called by anybody else it's meant specifically for the repository and so I basically wrote one that
basically checks that if you have this reconstitute method that's called by anything else besid a repository uh it would
blow up um that was not as straightforward as I thought it would be or I guess it was about as straightforward as I
thought it would be straightforward um so if we had uh our extract column that returned a result not of string but of um
what's basically a map entry right um I guess it could be a map it would be a triv you're talking key value pair when
you say map entry that's what you mean yeah so map. entry is actually literally a key value pair oh interesting map.
entry um but if we return to map that would be easier to comine could we pass the map into the next one yeah then it
just add to it is that kind of what you're thinking yeah so so the idea would be we'd stream over our headers and at
every step along the way as part of the map we would basically do a combine so we'd sort of do this C accumulator of of
um right it would operate on artist and it would return result of a of a map and then we'd combine that with song song
titles results and we get another result map and keep doing that back and forth and what we would end up with is a
result of a map of string to string and if they were failures then it would just that result would be a failure if there
were successes then we'd have that then that map would would values um the larger question is do we want to do that it
does seem like a lot of work maybe a lot of too strong it's it's not a lot of work um but uh does it bias it would it
would totally clean up this entire method right we would we would get rid of the duplication of 46 to 49 more than that
we would get rid of most of 46 through the into the method because it would accumulate our failures as well well right
so we'd get rid of 46 through 53 and then our 54 check would just be a check against the accumulated result um and we
would just return a successor or failure uh at of a result that takes a it's really more a question of do we want to
spend our time on on stream to do that uh or do we want to get get to something else um and I could do this you know
separately right right oh I just want to say DOTA to attitude I just noticed your your res subscription for 31 months so
thank you so um so punt on it for now I I kind of feel like it would it would take us a bit a field and and might I mean
it's not hard it's just going to take some time to figure out the nuances of how to do the stream with with the with the
combine and what the combine looks like and I think um I think we can we can just defer that should we add it in our Q
so we don't forget yeah let's add it let's add it uh uh what are we anyway skip over unused columns yeah I think I think
we could just pull that into a yeah I'll move it down but what are we going to call it um I think it's uh create result
combinator to help but it's not easy duplication to fix it's got a lot of duplication but yeah interesting we're almost
at the one hour point and I'm getting pretty close to meing a break anyway so apologies everyone on the stream we have
lots of breaks going on um yeah we could we could take a we could take a break now okay unless you wanted to I could
talk probably another minute or two if you had something you wanted to rip on um well I think now if we're saying that
we're going to punt on that uh I think we can say handle uh do we handle multiple themes I think um because I don't
think that was handle multiple themes I think that was handle theme missing because we must have had parse successful
parsing for for theme yeah parel for song with only one theme has one theme that's the second one up up top here yeah
done and I think pretty much 77 is done other than release type um which we said we're we're going to punt on looks like
yeah excuse me so if we want to punt on on that then I think the next thing is is uh database database and we'll have to
figure out what we want from that so take a break and then we'll figure out what we want from that sounds good yeah it's
just jir need to commit for jir I don't commit jir I don't commit to jir right all right so we'll take a short break and
when we come back um uh for those of you who placed Wagers on that we will do persistence today uh you win um so uh go
collect your your your your bets uh otherwise uh we'll see you in a few minutes and uh yeah see you in a few minutes
great e uh so missed this question earlier um sui ask we have results for optional columns where we ignore the failures
yes um so the column if it's not required uh and it's not there um the result is is success but an empty string and so
that way uh when we create the song it just accepts an empty string for for for that parameter uh so that that works out
nicely uh if you're not already a member of the Discord the Discord is a great place uh great Community for Java and and
any developer really who's interested in um the kind of stuff we do here on stream the kind of stuff I do on my solo
streams so that's uh testing test driven development fogal architecture architecture and design in general um domain
driven design all all those kinds of things we've got uh channels for just about everything you might be interested in
including XP extreme programming practices uh all that kind of stuff so join the Discord uh and just go to ted. Discord
and you can you can join up um we do have a book club um I think we're on chapter eight uh but I think this is the kind
of book where uh you can never you can never really join late uh so we're we're reading through the programmer's brain
and um we're currently looking at the the naming chapter so it's not too late to join um you don't don't feel like you
have to catch up and read everything you can do that as your leisure uh just do the current reading and uh you can join
and don't feel like you have to be active uh you can just join us we we meet on Zoom for a couple hours every Sunday
from uh 10:00 a.m. to to noon pacific daylight time which is what is it now plus 7 uh so 5: PM uh UTC and uh don't feel
like you have to join everyone but you're certainly welcome to even though we're we're already into the book don't feel
like uh you can't join because it's as I said and uh you may be familiar with um uh my test driven development game and
so uh this is basically a picture of uh some folks playing the game um the game is uh fun fun to play but also really
useful um for fostering discussion around around test driven development and it's very much centered around the idea of
of predictive test driven development that's one of the sort of the driving forces of the game um you can play it uh
Solo or you can play it with a couple people or you can play with up to up to six people and uh what's interesting is
there's a couple of different variations that that you can play um I'm about to uh uh update the the rules manual um to
add a bunch of those variations uh and so there's there's some really interesting aspects to that so if you go to td.
cards you can also see a video right there on that page uh where I talk about predictive test driven development uh and
then walk game all right and we're back yes so I forget what our repository looks it you probably want to open up the
code the main section ah there you go thank so let's let's take a look at that class and see what it what is what it
what it us so it pretty much allows us to uh create it with songs and then add songs and then get all the songs to um
sort of sketch out what we want from from a true repository um why don't we uh maybe in in the jira let's sketch out
what we want the repository to to do for us which might require us to look at sort of how we're currently using that in
our our application layer although I don't think we have much of an application layer uh got our song service that's at
got a final ho basically yeah so if we look at at at that ad song method so I think this is the this is the Crux of some
things that that caused us a little bit of a problem in the past um that we now I think have to have to face uh and
figure out what we want to do um we're basically calling ad on two different things so we're trying to keep two
different things in sync sync yeah and that's bad we don't we we'd like not to do that right so both in the and they're
both in the application later right yeah yeah I thinking No Maybe song search is domain right you're right right sorry
yes application yeah so we might need to to look at uh with the application layer we're adding a song we're adding it to
the repository and we're adding it to the Searcher because the search could be called to search well the Searcher is in
fact the the the thing we search against um right uh and so do we want um I mean let's take a look at at so it basically
builds builds an songs right so when we do a a look at one of the more interesting methods like one of the the search
methods so skip past this the static stuff right so there on 32 that's that's basically um 32 and 39 those are sort of
our our main methods and so at this point I think we need to decide do we want to continue having this sort of inmemory
cache of all songs uh or do we want to push this I mean the advantage of in cash is it'll be really fast um if we put in
the database then we don't have to have this duplicate stor in the repository and in the Searcher so that mean whenever
we add to the repository we have to reload The Searchers I mean I guess we could reload the searcher's cash well if we
look uh go back to to the song service right so if we look at the ad method the ad song method um what what in a sense
we're doing is we're saving it to our repository and then we're adding it to our cached data which makes sense right we'
re basically syncing you know we're we're doing a a you know putting it in the database and then adding it to our
inmemory cache and then we only look at the inmemory cache when we're doing our searches but if we go uh and store this
stuff in the database then we stop doing that we just ad song repository so it really depends on on back all right while
we wait for for Mike to come back and and solve his uh headphone problems um this it's funny it's like this is why I
don't like bundling things together uh whether it's applications or or Hardware I like I like discret pieces of things
that do exactly what they're what they need to problems can you hear me me yes and I can hear you yeah okay all right
took a few reboots there to uh reboots of the headset and streamyard screen all right looks good so if we add to the
repository uh so this part of the model I don't fully know how it works are we immediately persisting at the database or
only at a specific time or is the repository kind of like an in- mmory database well right now the repository is
literally an in mmory database right and so then the song Searcher is an in-memory cache of the repository in it's in a
sense it's it's it is actually the primary thing we we search for uh so we're always searching against this inmemory
song searcher um now from a dependency standpoint hexagonal we're not supposed to know the repository exists at the
Domain level where the song Searcher is correct and we don't and we don't would we just really be searching on the
repository and then yeah and then yeah so this yeah so so line 23 would basically be instead of uh executing that on the
song Searcher repository and if we did that would the it would still be an end memory are we loading no we wouldn't load
anything to we wouldn't load anything to memory it would all be any time you do a query it would hit the database oh
every single time got it yeah okay now there could be some some caching that the system does itself but we wouldn't we
wouldn't be in charge of of implementing that that cache gotcha ises that depend on the omm we choose to use or yes so
what do you think well I mean our current song Searcher doesn't do anything that we couldn't already do search because
it's pretty much give me um or give me the song titles which is basically give me the songs and then extract the titles
which is what we're doing right so literally the only method that we would need to implement in the database is is what
line you know what by theme is on Line 39 because everything else then that right um so the only thing that might be a
little a little tricky uh is is the fact that you could have one theme or you could have multiple themes um but that's
that's not how do we Implement that in song probably as a list well yeah in list it's it in in song It's a list um but
then when we basically index it we split it out into multiple pieces so we index it we basically for each theme we put
an entry in the map so we have dup we have duplicates and so what we probably do is um where was that that pository no
it's a Searcher that does that because the Searcher is the one that has all the the searching Behavior so it's basically
that that that it so uh in the database the way you do it is is you have another table so you have a a a one to many
table of song to to to themes and then you can search by then you can retrieve the songs based on right so it does does
mean we we throw something uh no I just wanted to to do something um so do we want to do that and then we then we
probably need to figure out from um from a technically from a a domain driven design standpoint do we care about
Aggregates um how how do we want to do that um right because it's really I think there's there's just one aggregate yeah
I think it point I think when we good farther down the line do you think it's worth taking a look at board I don't Yes
actually how about this You You You Pull It in so that way because the odds are high I'm gonna have to do another uh bio
Break um so that way you can keep talking if I have to peel away for folks who just joining I or I had a a medical
procedure where I have to go to the restroom quite a lot now today so let's take a look at this is at so this is um this
is uh the outcome of our our uh event storming that we did all the way back in in episode one uh so go and look at that
episode if you want to uh see see how we got here and so through this process we ended up figuring out that uh so these
things in this uh in this dark yellow are basically our Aggregates um and so we've got uh come on zoom in there we go so
we've got uh song and is an Aggregate and then user profile which we haven't done anything about yet uh is is a separate
aggregate um and then the whole idea of of proposals and change proposals and other stuff um these are these are here
but pretty much for song we've pretty much said it's it's the aggregate um and sort of how it's uh how it's represented
in the database detail and it looks like the other um well as there shouldn't be any dependencies between the Aggregates
right but in the context in which song is currently laid out there's how we do it seems to not matter basically in other
words we can still focus on song independently and not have to think about right anything else yeah because all the all
the dependencies are in incoming uh it doesn't have any outbound dependencies so uh so we're fine um So eventually this
idea a song proposal would have a dependency on song and so would have a a reference dependency an ID dependency because
they're separate Aggregates but um song does not know about its song proposals we don't we don't care about that at
least as far as we've figured out so far our event storming so unless we add new features yeah unless we add new
features we're we're we're we're good so um so then um I think how it's stored in the database it's we just store song
and and we let uh it's own table I mean we could we could start with with putting it in a single table and I think we
can just just make it uh embedded meaning like a column with because really it makes more sense to to go with um like it
would be an optimization from a from a database standpoint to have themes as a separate table if we're going optimize
basically sort of make make theme more primary object and basically theme then has references to all the songs and so we
take a theme and it has basically a list of uh uh songs that it has references to versus it just being a separate well I
mean table our usage model is mostly give me the songs based theme or is this premature optimization I think it's a bit
premature because what so it's the difference between um hey database find me in the theme table find me the theme okay
I got the theme okay now for this theme find me all the songs you've reference okay and so now now it's it's basically
got a bunch of bunch of rows a bunch of IDs to songs and then it basically then grabs all the songs versus just look
through the song table and find the rows where there's a theme in in the theme column um for the size of our database I
think it will will be uh not something that is is noticeable we'll need that yeah and would the theme column be like how
we separate the themes would you be like a a blob or like semicolon separated or something like that yeah that's that's
a uh a good question um I mean we could do it as uh have some kind of separator and then search for it that way um
there's probably more efficient ways to do that um um there is uh like postgress has an array column that you can have a
bunch of items in oh that's cool um I think we'd have to we'd have to see how that works out but I think we're if we're
if but that really is a database detail implementation that um we probably don't need to worry about at this point
because we've got work to do to to basically move around the code uh so that the repository is doing Searcher so from a
unit testing standpoint will the searching be at the repository layer or yes and it'll be but actually in the production
version it'll be in the database that's where it's happening well it'll still be the repository implementation it will
just be a different implementation got it so so we'll need to extract um we'll need to um basically move behavior from
song song Searcher to repository um and then extract an interface and then that interface uh will'll already have the
inmemory version because we'll refactor to that uh and then we'll have the concrete uh database implementation that will
also Implement that same repository interface sense so let's switch back to your code give me a second and actually I'm
probably have to peel away again all right so if this is becoming too frustrating for folks I totally understand um my
screen's available if you want me to put it up and then I walk do um it's really not a a on to many mapping we're
basically saying that uh song is going to be a table and it's just theme is themes is going to have uh screen so I don't
know if embedded is uh because we're not basically mapping so song is the entity we're not saying that there's multiple
that there's another entity called theme we're not raising theme to the level of of an entity uh it's essentially a
value want on is is query I think it's going to be pretty much something like this so basically find theme find by theme
in and then it's uh no we want the other way around we want containing and I think we could we could figure this out
this out later I think we'll we'll assume that there's some mechanism and we'll just write what what method we want uh
and then that'll be our repository so we know what we can do as possible it we'll just have we'll optimize later gotcha
so we'll we'll basically work on moving song Searcher into repository yeah have the that implementation which is is fake
the correct test double term for that yes yes so it would be fake fake and we get it all working for that and then from
that point we then work on you know how will we use this the spring relational data stuff right right so let's go back
to your code give me a second I get my screen back in say order again here we go so let's let's put let's put down our
notes um uh in in jera so I think the so the first step is move thong Searcher repository and uh once that's the case um
that means we should be able to then uh extract interface extract a proper interface extract a port interface for song
repository uh and adapter it's tempting to almost not even bother with spring data jtbc and just write write SQL um but
then there's a lot there's a some boo plate that we'd have to do um I think those are the steps so we certainly won't
won't get through all these today uh but let's so this is um this is a refactoring we're not changing any any external
Behavior Uh from the point of view of the song service layer from so from the point of view of the application layer
nothing is changing um but we will probably have some internal tests that yes so from the point of view of the song
Searcher that goes away um so from the song service inside uh stuff change all right suiga have a good night hi sui see
you next time so um yeah so I think let's let's start moving our Our Song Searcher Behavior repository should we move
move this to yeah so um I I think we should sort of a in a sense a parallel change kind of thing um I mean let's
basically extract let's extract that for loop from a line 11 meant the other shortcut yes and now I got to reselect uh
so expand select is is probably better yeah because that doesn't that was too much that was too much so control shift W
will back off but you've moved the cursor to the wrong place making a big rest there rzy okay one more time uh you gotta
undo because something went wrong yeah something went horribly wrong yes okay W there we go yeah and what did you say uh
let's just call this index because that's really doing index songs Maybe well songs is the parameter what else so what
else would it be indexing true and this this is going to be somewhat temporary anyway so I'm not too worried about it um
let's uh since we're going to be moving this code to the the repository which doesn't have an array it has a list let's
change this index method to um uh to turn the array into a I don't know what to call it else for um is there a direct
mapping so like there I think so uh to array no to list yeah so we could do a stream to list I think we can also do um
arrays. two list I don't know let's arrays so backup did you hear uh Delete well we don't want songs there we want
arrays five hour sleep yeah so hit Dot and as list yes as list and then and then songs yeah control little cheat Che was
off screen code completion Al shift shift enter control shift enter in mine you said alt oh I don't know what it it's
it's command shift enter on on on Mac I don't I always forget what that translates to okay yeah control shift enter here
too yeah it's control shift enter uh and so then let's change our iteration on 16 instead of going through list just a
direct replace yep that okay work should we switch to all or IO free still uh I think I IO free is fine yeah um so now
let's push out let's introduce parameter on the list so uh because now we want song list parameter was it Control Alt p
uh Control Alt P yes okay so now we have a method that takes a list of song and so now we can basically copy and paste
that into our repository where do you want it after create yeah let's put it after after create right here okay um
actually let's put it after the Constructor because we're basically going to merge it into the Constructor for all right
uh and then let's um let's just leave that there uh let's move now the behavior in song Searcher so the searching
Behavior the B theme method move or copy um actually let's yeah let's copy these three methods three meaning which which
ones the ones that are on screen all three oh got it to there y right after index or somewhere else um let's put it at
the bottom yeah so it's probably going to be a fct uh that's fine let's um let's delete the the ad on the top because I
don't think we're gonna want that one the one we just copied so the last this one no last the one we added the one we
copied oh this one yes delete because what we're trying to do is we're trying to basically make this have the same
methods that our Searcher does and now we're going to retarget uh uh our Searcher you don't have to be by the way in on
the name of the class you can be anywhere in it oh really and just do um and then just do actually I was doing controls
shift but uh what is the yeah control shift T control shift T right so we get two so let's go to the there so that
creates it adds it does a by theme similar for the next one um so what's the difference between the class theme song
theme Searcher test are they in two different domains or one's in the adapter oh one's in the uh yeah then we just want
the song Searcher test great so let's take our song Searcher test um Let's uh to the let's yeah let's swap our things
and move the song repository to the Bottom now because we don't need we're done copying stuff so we can now arrange it
all right so let's take our song Searcher test basically figure out how to change it so instead so I think we repository
me make repository a little bit bigger there's the Constructor but that's private there's a create which takes a list of
songs static empty that's it so what is our test actually doing the one that's testing Again song Searcher yeah uh so
let's create empty and then we'll do an ad so let's just change all of our song Searcher there to repository like this
yeah okay and then fix it and just create that method no no no we want we want all the code is is already in song
repository so we just need to change change things here's what I want you to do I want you to delete 16 and 17 and we're
going to write it from scratch got it okay so empty yep and then hold hold on to it public no it's not uh let's make it
public it really there's no reason it Y and then uh instead of against song repository did you want to rename the method
I mean the local variable song repository or is repository good or no uh I kind of like song repository okay yep so um
this will fail because our ad isn't actually adding it so that it's findable by our B theme uh so that's fine so let's
run it and we expect it to fail because it won't won't find anything run just this one or the whole no all all of them
because nothing else yep all right so let's make it work y hello Mr camera you don't have much to say so what we're
doing here is we are moving behavior from song Searcher into our song repository and preparation for for our split so
that we can then have a database implementation um and this is both a refactoring and a change in Behavior so it's a
refactoring from the point of view of of Our Song service and um a diagram might be useful here so let me go diagram yes
in fact I do so let's go that so this is our our sort of design for for our current application right now um our web
adapter which is what we see on in the UI when we want to search for a song it calls the song service song service is
what we call um our application layer or our use case layer uh and currently it is calling then song Searcher to do the
work um what we're going to change it to do is instead uh the song service is actually going to duplicate this and we'll
call repository oops and this will become basically a database adapter uh so for now it uh song repository will
eventually become uh what we call a port in in ports and adapters or hexagonal architecture and then we will have a
concrete implementation uh out here let me draw one of those uh and this will be purple and I always find these images
that's the app I want to work on next so I've got I've got two things I want to work on next one is is uh a very plant
uml like way basically text to diagram and I'd like a text diagram for this um so what we want to replace this with is
basically uh song service we'd like to talk to uh why not letting me do that could you move the repository at it I use
the arrow because that's actually what I want that's what I want ah the line apparently doesn't have a way to to do that
but arrows um so what we want is instead of this direction where it's talking to the song Searcher that's inside of our
our domain we're basically saying we're g to push all of this Behavior into the repository and so we're going to end up
with two different implementations of this one of uh post crust um but the one we're going to work on actually I'll
duplicate this is our fake uh in memory implementation and that code already exists it currently exists in uh in song
Searcher um so we're basically moving our fake and that's uh that's how we'll get our fake and so then song Searcher
will go away um and so basically our the sort of the line of here so everything uh everything sort of this way nothing
changes everything on this side of the line we're basically now retargeting so we're now having song service talk to
song repository instead of talking to song Searcher and this rotation is annoying me there we go we're basically moving
to a really thin domain object yes we are Bas yeah we are basically moving to uh almost no no domain Behavior which may
seem like it it then is overkill for hexagonal but we've got other behavior that we'll be we'll be pulling in right so
then later when we do the idea of song proposals and profiles right that okay so we left off um you were asking me to do
something and I forgot because nature um the test P the test failed and so what we want to do is oh we might make it
pass right right uh we'd like to make it pass so let's look at our our by theme thing right so what we'd like to do is
the the problem isn't here the problem is we're not updating our themes theme to songs map right so let's let's do that
I think we have a way of doing that would that be at the ad song call the oh noit that's just song TRS yeah yeah yeah
that's right so um we want to add a a a call here to our index method oh to index right because we basically have now
reindex wait a second what's index taking it's it's taking our have we do yeah we're referencing it on line 40 we added
the song to songs and now we want to index that songs which looks weird because like why are we passing in songs to a
method because we method yes now I get it why it's looking work and it did uh so let's clean up that that index method
because that so what we can do is basically remove that parameter this one just reot force it like that yep and then 18
songs right doesn't need sorry uh and did you fix the collar oh whoops well actually we I didn't manually do it that's
what I did so I should change signature yes ah control F6 Y and Justus move it refactor yep and work all right uh uh so
now our test works so let's go fix the other test and retarget that test right so is fix this one yeah so 1617 control D
is your friend for duplication in case you want another shortcut I know that when I Su my at the front of my was it
short-term memory um it's not well it's all on your longterm memory it just isn't as accessible as yeah it might work
assuming assuming our are we're calling things in the right way it's very inefficient create song create song uh so I
think the we've seen this problem before when we when we did indexing so let's go and method so really what we want to
do is we want to um we want a new map every time because we want to re we songs so we want to do is uh clear the index
uh before we before we do any indexing oh yeah it yep y so again this is this is not terribly efficient uh because every
time we add a song We're reindexing um but this is a fake implementation so we don't care and maybe we will optimize it
right now we don't care all right so um we should probably rename this test class now is there there's already a song
service well this is this isn't testing S no it's repository yeah yeah do we have a repository class this class is it
Control Alt T no be create new one so we just rename this one to commit so all we've done is we've moved the behavior um
but we actually haven't moved it we've merely copied it uh because we have not yet retargeted our use case layer so but
now we we have basically the behavior that song method actually before we do that um we copied over the song titles by
theme method um but that test wasn't using it um so what is using it yeah what is using um I feel like that those test
methods should be in our repository test repository test yeah you just move them all over or copy them over uh let's
just um scroll through it just to to take a look so this one is doing song Searcher yeah okay and the next one is
parameterized song Searcher okay that one's that yeah I think we can Y and let's one by one just change them someti
boiler plate um search for theme does not exist results so here we're creating empty and uh this is this is a bit more
nullable like than than I tend to do um and that's that's and I'm wondering if we want to stop doing that yeah it seems
a little bit because this this is purely for for for tests right um so let's grab the the song part of it because that's
that's all that matters we can grab the whole method um and then we can class like that yep uh and what it's going to
return is not a song Searcher but what we want is Repository change signature or just manually do it just manually do it
because that's there's nobody's using that one right uh you don't want to rename you just want to delete and right and
then do whatever we need to do I imagine this I don't know what is the Constructor it might be a private Constructor
yeah so the Constructor is private so we probably want to call a static method on it instead of yeah get let's just
create with a list of you need to wrap this in a list yeah or you could say create empty and then just do an add that
might be easier one PR too it yep and then let's call it from that test above it above oh above uh oh sorry no I thought
it was above it it's uh no you want to call just the static yeah no so online 46 just delete song Searcher Del delete
everything from from the declaration up to the width so start at the left edge of 46 okay and delete all the way until
you get to the width ah got it and now delete the variable now Al alt control M uh alt control V al control V oh that's
the other one alt contr V oh okay cool that's what that's what dovar basically does is uh introduce no just hit the down
arrow a few times yeah Y and let's see if this works it should because that method is just dependent on by theme uh
other than syntax error where was that ah there is so control shift enter will should should great let's just do the
same thing for tests so this is new song search song so let's make this also um another local static method this guy uh
no there's no point in copying that it doesn't provide much useful for us okay local static sorry so let's uh let's
delete everything but the oh no wait a second yeah that's okay y yep and then song uh and let's where's our static
method the one that we just created which one the this one yes um let's extract out uh song from line 40 so we're gonna
generalize this never mind I could have done this to a local ver up meaning like that uhhuh and now can extract 40
through 42 into another static method 42 40 through 42 ah and this is uh create song repository with y song uh oh I
thought that's not the test that's not the test we that like that but without no no you got you got it wrong I'm sleep
deprived and having to go to the restroom all the time okay lay it out on me uh so undo until you get back to to working
code there so create song is fine uh what you want is on a new line call the method that we just that repository work y
uh so we looks like we skipped a test back uh did we oh no okay I thought I thought we skipped one but that's fine yep
that's long repository that's long repos repository then the next uh let's do the same thing yeah I'm gonna step away
again sorry okay all right I'm gonna actually take a proper great e all right so while I'm waiting for uh Mike to return
uh as a reminder um I have a Discord and encourage you to to join go to ted. at Discord sorry ted. Discord you can join
the Discord uh and as I've mentioned uh we run a weekly book club on Sundays we uh get on Zoom for a couple hours and
talk about a book we're currently reading the programmer's brain uh currently on chapter eight but as I like to say
there's uh there's no bad time to join a book club it's never too late um it's not like you have to catch up a book like
this especially is pretty easy to to to jump into and just read the the current chapter um there's not a huge amount of
reference to Prior stuff so uh if you do want to join the book club and you're not already in it uh go ahead and hop on
the disc ORD and send me a direct message and I'll add you to the the private channel that that's my little level of
screening to make sure that that you're a um and I have a few copies left of my tdd game uh I'm almost out of of copies
I have more on the way being manufactured but right now I only have a few copies left so if you want to get your copy go
to td. uh play this tdd game um it's great for uh teams to to talk about and discuss it's great for for folks who are
teaching tddd to others or talking about tddd with others uh and it's a fun game in its own right um so you can see a
video if you go to td. cards you can see a video where I talk about the predictive test driven development cycle that
underpins the game uh and then actually walk through the game itself and so you can get a an idea of of how that works
so that's at td. cards go ahead and and take a look at it the video there uh walks walks through all of that that's
basically the process that we use here on on the Stream So notice when before we run a a test when we expect it to fail
because we're building new Behavior Uh we do do this precise uh prediction and that uh does a lot of really good things
about making sure you understand the code and making sure that uh the test is actually assert and so we're um we're
using uh hexagonal architecture and so one of the complaints that that I read about um and there's some folks where I I
hope to be able to talk to them at some conference where people say that hexagonal architecture is is overkill it's over
engineering um there's nothing to it that's that's over engineering uh so it's really an interesting discussion uh
because this is it like what we have it's basically just classes where you're very clear on what their roles are you're
very clear on what their job is so we've seen here in our um diagram which represents the application we're currently
working on there's not a lot of classes there's not a lot of of sort of extra code I mean even if I wasn't sort of
organizing the code in in hexagonal architecture we'd still have separate classes for this stuff we still have a
separate class for our controller um possibly multiple controllers uh we'd still have a separate class for the song
service because it's going to be the one that's loading and saving from the database and we'd still have have our domain
objects that have have the information uh what is interesting is I think many people when they see these diagrams it's
like oh that's looks so complicated but then when they look at the code it's like oh that seems straightforward what I
think is really important when you think about these kinds of architectures and these kinds of ways of organizing code
is the benefits so there's not a lot of extra things that you do other than what you might do normally but what it gets
us is our tests are fast so when we run tests here right our use case layer tests they run fast because everything
inside this hexagon is completely free of IO there's no IO code in here and so that means when you run your test they're
going to be fast and if you're doing tdd that's what you want you want your fast running tests because if you have to
wait 30 seconds a minute for your test to run that's too long you want really fast feedback Cycles because you're'
taking very small steps you're reading one or two lines of code at a time and so this is uh what we sometimes refer to
subcutaneous because it's just below the UI right so this class here represents the UI uh but this test is testing just
below that and then we can write tests against the adapter code directly and we do that but those are slower tests so we
don't need to run them as of and so you'll notice when we're running our tests here on the stream we're running
basically these IO free tests um so they're testing the song service and they're testing any domain layer test that we
have and so when we're testing Our Song service and how it works with our our fake this is where test doubles come into
play we're not using mock we're not using using uh a mocking framework like makito because that slows your test down
makito in order for it to do its job has to do a bunch of stuff underneath that basically slows down your tests and it
also tends to make them very hard to read so instead we basically handroll our implementations and then once we have
that working and so we we now have our service talking to the Repository then we can swap out right and this is the job
of a test LEL we can swap out this thing uh which we will certainly not not get to today uh but we will once we finish
swapping things out we will have a proper separate uh inmemory adapter and this is a port Our Song repository is a is a
port so I'll color it actually I want s that color yeah so that's that's I mean if again if you look at the source code
there's not architecture so I I encourage you to I've got a bunch of videos on my YouTube channel um one of them talks
about uh hexagonal architecture um and basically how it makes makes your code more testable so I encourage you you all
to to watch that all right uh Mike you're muted there you go just to cause trouble yep all right so let's continue um
moving our retargeting our tests so that instead of talking to our soon to be obsolete song Searcher we're talking to so
this one we're going to do the same thing too so since this one takes multiple songs we're going to need um to have uh
to extend our static method that we are referencing on line 70 to have uh the ability to handle multiple songs so let's
let's do that refactoring now and then it'll make it easy to uh extend that instead instead of song It'll Be song dot
dot dot ah do it that way but as a signature yes uh no you don't sorry you don't need to do a signature change because
it it is so you want to change not that one oh the other side it's it's on the type yeah of course so that's a fully
backwards backwards compatible thing from the caller uh and now we just need to change so what I would recommend is
rename the variable from song to songs and then we'll be able to to wrap line 47 with a for Loop ah can we do surround
no uh you can do surround but not uh not with a postfix W so what you want is control alt t five it's number five in the
list but it's the four oh it's like no not that four the number the number five number five four four which is four yeah
uh and then we just want to Loop through the the songs so um this is old school loop right no no this is New School y
this is basically for sorry song song and then songs okay yep and then we can change that how that songs oh I renamed oh
okay there we go that makes sense so now everything should still keep working everything should still that should have
been just a prepare refactoring yeah and we're good y then we go back to and I'm gonna ask you to delete line 47 yeah
and now we're gonna go back to the the test took multiple songs this test yep right right so we're going to do what with
you can pretty much just copy um so scroll up a bit yeah right there so no back uh if you copy line 72 everything up to
the open print for for width yep copy that and then go to our test and then delete 82 and replace it yeah oh right
because we did dot dot not this okay right right right and then this will be song repository right uh I don't know why
there isn't a blank line before 85 but let's put one in because that's what we're testing so work yep and then we can
continue doing that then the next one you pretty much do the same thing as you did same thing yeah she might still be in
my buffer buffer to to the end of the line yeah to there nope oh right because I had changed uh so you can do uh control
shift V because it's in your buffer yeah no that one and I got an extra left for because as you said earlier we're
retargeting yep and is that the last one uh no I think 109 is the last one yeah I model that yep extra line oh we got
another test below it oh there is a test below it okay okay may as well fix that one while we're here oh I already ran
it but all right that's fine it's fast as I was just saying fast test okay same idea actually the whole Time y yep uh
when we have a line here yeah I think retargeted actually it's more than retargeted we copied we we copied uh tests for
song title search test we copy or move I think it's empty oh we may have moved yeah so we could probably delete that now
so let's yeah copy test oh I forgot the name of that file though uh it's right thereit a second song search by theme
well we moved moved yeah it was it was copy but we realized we moved it yeah yeah move test to I like to be dramatic
like a movie okay yes um yep we did that and then we retargeted well I think that's implicit in really because of the
name of the class yeah test class okay yeah cool commit it's a small commit so I'm not worried if there's if if we are
confused later on if we ever look back at history I think we look at it the diff and it's obvious yeah all right so we
deleted the other test um let's go into song Searcher and see who's using it because probably the only thing that should
be using it well the production code still is because we haven't finished retar we haven't retargeted the application
layer right um but we shouldn't have any tests that are using it so the only things that's using it is basically line 14
what is this one usage was filtered out uh I don't know click on it let click on it see what that says that's
interesting might have had Constructor I don't know yeah why was that's weird yeah um so now we should be able to swap
out repository for song Searcher uh here's where we're probably going to want to run all of our tests because there's
going to be some depend pendency right yeah so everything works fine now out just start there's only one place at the uh
service yep so would we just rename this repository or change the class no we already have repository so we basically
want to uh change the call to song Searcher so wherever we call song Searcher so let's look for the references to that
field okay there it is online 23 oh 23 so if repository and we run all the tests that should still all work we didn't
really have to run all the tests but I thought we might have a dependency change but actually song Ser song service
already had a dependency on the repository so now we got a broken test uh good um so that means uh so we replaced the
call to buy theme we didn't replace the thing that loads the or causes the the repository to to to do its work odd let's
let's look at the test that actually failed yeah let me go back to that no that's not it oh you'll have to rerun you
might want to close that notific test so does this test still make Startup what does that even mean so on Startup oh I
think it's saying that on Startup whatever songs are in the reposit are loaded in so let's look at that create method
there on indexed Constructor so let's look at the Constructor ah so we never called index from our Constructor great
let's call now that should allun the test yeah we can just run the io free at this point oh oops next now pass all
Searcher so let's well let's let's go back yeah let's go back to song service um so we should be able to delete uh all
the usages so let's delete that 27 and then we can delete the field and then run our tests and it should still voila
voila vo uh so now the only references to song Searcher are itself and which means we it interesting how it doesn't oh
wait a second server still has it as a import oh there's an import so just optimize Imports does that explain why it
wasn't gray now it's showing gray so now we can do a save delete yeah um Searcher to I don't know deprecated better
repository I like that commit yep yep all right cool uh so let's go back to jir and issues so yep first J 88 is done
should we extract Port next um or you fading or well that let's let's let's take a look because I don't think that'll
take very long yeah it's it'll mostly be deciding what methods we out okay uh repository and actually I probably right
so what we've now done is we mov the behavior that was in song Searcher into uh uh Our Song repository implementation um
and now what we're going to do is we're going to basically extract out a port interface uh and so this is we'll see that
the hard part is figuring out what do we expect the repository to support um and what we expect the repository to
support is finding songs that match a theme um the thing that basically gave us just the titles for that uh which is the
test we just updated uh that's not something I would necessarily expect the repository to do for us um I mean we could
uh but that's sort of a bit of a transformation of information that might not even belong in in song service at all uh
so we'd have to see sort of what what uses that if it might just be something that um that that goes up here so one of
the things about uh hexagonal architecture reports and adapters is this idea of transforming or translating or uh
converting I I prefer the term transforming uh things in our domain so our domain objects right so like song when we
want to present it um we may only want to present the title or maybe we want to present the title and some other parts
of it um but sort of this idea of converting it to strings for presentation that is outside the hexagon because that's
very specific to what is the purpose of this adapter um because the presentation that we want for this adapter might be
different than the presentation we want for some other adapter that we might create so this one currently is um
presenting through a controller uh but we might want to have an API a restful API so um that that might be uh and that's
why this idea of having the adapters do the transformation is because how you want to transform domain objects is into
something presentable depends on how you're presenting it if we had API then it's going to translate it differently
because maybe it wants to create Json so that might be um some other some other adapter maybe out here I'll put it now
so we'll have to see where where that goes all right let's switch back to to your screen when you're ready so um were
you answering uh vegan A's question uh that wasn't a question oh right right right that was just a comment um so let's
look at uh basically what methods we we have pretty much there are just two methods that are part of the what people use
song repository for which is so we've got all songs do we use that can we take a look at who uses tests okay so I don't
think that should necessarily be part of the repository interface we'll have to see um so it's basically add and uh who
so who's calling song titles by theme what non- test code is calling that none anything maybe we're using this one at
production controller does the service call the controller I mean the controllers call the service the controller calls
the service so it must call that method and so therefore uh what can we open up the controller yeah it seems oh we what
do we call the oh there homepage ah yeah we do call that why wasn't that showing up that was weird so service yeah so do
a control no go back oh okay do control here oh the it looks like it's a test because it's got a oh so it is okay so it
is yeah right so when when you do it the dark blue cursor yes it it sort of H hid the fact that don't see that it's
white yeah yeah okay so that's good so how the brain interpolates that to being green underneath the blue yeah yeah wow
fascinating so um so if we're only using it for tests we can decide later whether we want to do something about that but
that means really the only thing we need from our uh interface is ADD and by theme um uh let's rename by theme to be
fine by theme because I think we lost a little bit of um stuff when it used to be called song Searcher it sort of was
nice song Searcher by theme but now let's let's make it called Fine By yeah I like that hit enter yep um and now let's
yeah there's no shortcut for that one well there is but not directly to it and you don't have the the nice and easy
control T that we have on Mac gotcha Al so I could have done control shift alt T yes and then go to extract interface
and then five yeah that's typically what I do so we want to rename the original class and use the interface where
possible and we want to rename our implementation absolutely and have the interface be I song repository no uh this
should just be like in memory song repository I thought you gonna say fake okay no I it's it's it's a it's not actually
a fake so there's a difference between a fake in memory is that because this actually could be used if we decide not to
use a DAT yes because it actually is is 100% fully functional right so it's not because it served as our implementation
for for 27 and a half episodes right um oh that's yeah so that's better name yeah so uh so we want to pull out fine by
and add uh uh I think that's it and everything else will stay in the concrete class but W be in the interface right okay
um okay uh oh well I can undo no it's fine it it put the inter it'll put the interface actually the interface might be
in the right place where did it put application yes yes Port Port so oh right here right there oh that's yeah it's empty
but it's there empty yep uh so let's go ahead and run our tests I don't expect anything to to have changed yep um let's
so I think the last thing we need to do uh is yeah so that's our Port we have a concrete implementation uh can we go
look at um repository is there a way to go to Just instantiate versus all usages uh I think help it's line yeah so who
calls that create method no who calls the create method I know I thought that was I don't know why wrong and the first
line is production C code the bottom two t so uh let's go to the that uh empty so who calls create empty is the startup
okay Service uh why is the service doing that can we look at that oh that's for create n okay so can we go to the
startup code yes let me go back to I could do this you can just do control n control control n up y right so this will
have to change at some point uh but for now this is fine um because we're we're basically saying when we start up we're
going to use the inmemory version at some point when we actually switch over to production usage with a database then uh
we won't do this anymore um but for now that that's totally fine so let's run all the tests just to be sure and I think
we're we're day cool all passed yep all right uh is there anything uh so we extracted the inter face we can check that
one off so done uh and I think we can add one more item so before we implement the jdbc adapter um we want to make our
inmemory version act a little bit more version uh actually it may not matter in this case because we are not modifying
songs just yet so if we were modifying songs we would have the issue of there would be a difference between the database
implementation the inmemory because the in memory would see changes to song that the database would not see uh but for
now I don't think there's going to be much much to do okay so commit let's commit okay boy we changed a lot I think it's
just mostly because yeah anything else I think that's it okay well oh it's saying commit check or some in okay cool all
right so that's it for episode 28 um and uh so for those of you who placed Wagers on whether we'd get a persistence
today you win um go and collect from your from your well did we say their database um that's a good question you'll have
to talk to you'll have to talk to your bookie and figure that out because that may be ambiguous yeah maybe it's
depending on how big The Vig is yes um so next time uh on our next uh song themes episode we will then actually uh
figure out the the database table stuff the adapter um how we want to write it to the database uh uh we'll be creating
dto for that uh and we'll continue test test driving that um and I think once we do that we probably want to redeploy to
production uh because we'll have to modify production so that it there actually is a database there right um and so uh
we probably won't um I I I put the probability of us getting to that point at in the next episode at pretty much zero uh
because there's still some some some work ahead of us um but next time we'll we'll include we'll pull in our our
postgress and spring data dependencies um we'll also pull in Docker compos and our test containers so a bunch of that
stuff that we haven't had to deal with uh we will now have to have to deal with and we'll do that we'll do that next
time cool so as always thanks thanks folks for hanging out and chatting and uh asking questions we always appreciate
that uh join the disc if you're not already there can I give a pitch yeah go for it so at the volunteer radio station
which where I volunteer is this one k Alix um. berkeley.edu we're doing our annual nday fundraiser so if you want I want
to support local nonprofit Community radio all volunteer run um check us out listen to music if you like it if you like
the station press the red donate button so what's the URL for that oh uh kx. berkeley.edu donate if you want to go to
the Donate part but if you just W to listen to the website or look at the website and stream we drove lers all over the
world there you go that's the the upside of the of the of the web yeah exactly all right so support your your local uh
Community radio and uh otherwise we will see you next time um I will probably have a pairing uh sorry solo stream
tomorrow probably uh and then our next pairing stream will likely be sometime next week we'll figure that out the
Discord again is the place to to go to find out and to chat about all this stuff so so join us there um otherwise
