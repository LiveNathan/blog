# ＂Song Themes＂ Episode 36： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=Jxqqc4HqT1o

---

## Transcript

all right hello folks welcome to Tuesday how you doing Mike good welcome song I bet you have a theme for songs about
days of the week oh yes there is I don't think it's in the spreadsheet but files uh so last time we uh were able to
search through some themes and gather the themes together um we got basically a list of some of the themes so even uh
but you know again we're doing sort of baby steps small steps um so I'm G to share your screen if that's when you say
some of the themes I'm confused about that yeah so let's take let's take a look uh let me switch us to that there we go
um so at the bottom note that on line 11 uh we're doing uh the one so basically we're Gathering all of the first so
we're storing the themes as an array in a column and so this sub one is basically because it's one index based as
opposed to zero like the rest of the world um at least I think it is uh actually I know it is because our test tell us
um so we're getting basically all the list all the themes from the first entry uh and ignoring all the other ones um but
that was fine because that was uh again this you know very thin slice of let's just make sure we can actually retrieve
individual themes get them all the way out helped us Define this new outbound Port the theme finder uh and then allowed
us to implement the concrete one and test drive it all the way you notice I just modified our jir yes yes we had checked
off list of all things yes which was technically not correct yeah that's why I mentioned it yeah so let's say hi to our
regulars hello Jonas welcome Hey Jonas and astred nice to see you welcome uh so our next step is um as always after sort
of a very generalize so um in order to to generalize we probably want to write an update our test or modify our test
must have been this one JBC theme finder test I'm just guessing that's a that's a reasonable guess yeah yeah I want to
close some files here sure I don't need that I don't need that config what is that anyway oh that's that okay yeah yeah
yeah okay theme finder we've got one test all themes returned by find all for single themes so now what's interesting is
that one is oh because they're all the first entry right right I was gonna I was going to point that out specifically
like the first someone had money and donate um maybe we let's add uh uh let's add some more maybe to like the third one
just to add another theme after after daddy as a side note uh chat GPT is apparently down so people around the trauma
as's like no we decideed we're not normalizing we had a whole discussion about normalization last time all right so that
that test should still pass despite the fact that we added uh the second the second theme should I run this one just as
the class or uh yeah no one that's right Jes say who wants who normal excellent okay pass so now I presume we're going
to crank it up and have it yeah so the next step would be uh uh we'd like to get what five of them uh order the order
will be interesting um interesting money money because we're not dealing with uniest yet yes we're not there we haven't
done the unique part yet yeah you think we should do unique first before to I cuz then we don't need to well I guess do
we not need to I kind of would like to take the I it doesn't matter too much um okay I'm just not sure how it's gonna
come out when we do donate would donate go here well I mean we we could say we don't care about the order because we
don't or we could guess that the order is likely going to be uh uh row oriented so money donate money daddy heart is
what what I expect yeah and that could be the experiment yeah that's what that's what I was thinking is like we'll learn
what what it is that's my expectation because we're going to do an unest on the array which should flatten it but we
should still be getting it row by row oh that's not true ASD if you're here you are extraordinary absolutely so we
expect that to fail not in fact it says so but could not heart yeah yep uh so instead of Select themes uh Nest like that
uh it looks like it's most people do it lowercase because it's not a SQL command it's it's actually a function uh and
then in parentheses you'll P you'll pass themes and you'll brackets and yeah just no no leave the rest nested we have to
Nest it um let's see so we unest that returns it sort of as Docks do you want to share screen with what you're looking
at uh sure first why is that's the old screen so I have to say it's really it's really interesting I've been doing it
was uh I thought I had written down what what the right commands were um but I didn't and it's it's really fascinating
to me I know this is a bit of a tangent but like this comes up as the first response like oh that looks good onest
functions you know syntax and and a and and essential queries and all of them are just like here's how you just unest
the array not what a full command of what you would typically do which is unest an array column in a in a row uh so it
does this but that's like you're not where you're retrieving that from so it's it's got this inline thing so I
understand that okay you know want to show it a concrete example um and then they show another one okay another concrete
example concrete example are great and then like two-dimensional stuff it's like all of these examples it's like none of
them are showing here's a table and here's how you extract it all of these examples are just like we're gonna in a sense
pretend that there's a table that has this this data in it and conclusion and then like okay but but but how do I do
this how do I use this and and this is this is sort of a case of like like what problem you trying to solve here what's
your what's your audience what are what what are they trying to to do um and so this is complete that was completely
unhealthful and that wasn't the only one I came across uh where was it uh this one is different this a stack um and it's
just a different situation uh but like it's it's um like how you how do you unest okay but but you're unnesting you're
not just unnesting an array you're doing it in the context of of a select right um and and so uh so the post credit docs
uh these are the array functions um and so you know this is this is sort of typical for for reference Doc it's like okay
unest any array uh but you know reference docs don't gen you know unfortunately don't generally have examples and so
they're it's if you know what to do and you know and you're familiar with the structure of of of SQL um it's like oh
this should you know be be all you need um this one as well it's like okay great I know how to use unrest unest and
again like showing a hardcoded example and another hardcoded example and another hard-coded example and another
hard-coded example like are they copying from each other right it's like finally example number five how do you use
unest function on tables data which is which is to me the number one thing that you would want to do uh and so it's
basically uh so we unest looks like we just unest and I think Jonas already gave us that so let's switch back to you
make but but it's like why is that the fifth option why is like that the fifth thing it's like here's so the way I would
write this and maybe I'll I'll write a little blog because I keep forgetting how to do this is I'd say here's your table
here's what you want to do and like if you don't know how to store arrays in tables okay great but that's a different
question so let me share your screen uh so we want to do uh we want to do select unest and not start from we will need a
star from later on uh when we need to do uniqueness but for now we can we can do that uh and I think that's what we want
so it'll unnest and expand it but what we want is as theme so we'll get we should get the individual themes um so let's
try that so I expect it to pass modulo maybe it's out of hey look at that it passed Cold Cold Heart pass wow um lucky us
uh uh yeah if if you ever want to get me on a rant show show me like examples that are terrible or or non-helpful but
again a lot of it is about you know like I'm not necessarily ranting about who these people are and what they're writing
they they they may or may not have a specific audience in mind um and this is why I always encourage folks to to write
up what they learn because your point of view and the thing you needed answered might be exactly what somebody else is
looking for uh so yeah all right um so we hey we can check I'm glad you showed us all that stuff yeah I think it's rant
was valuable I think yeah I I I mean I I sometimes forget um that it's it is really useful uh for us to show like how do
we figure stuff out right as well as ranting exactly both are yeah clearly I uh I don't rant enough because I don't have
enough views you know content creators really spend zero effort I don't know if you heard that from the CEO of Spotify
he just said basically they it takes zero effort on their part to generate to create music and stuff and it like h i see
it was like all right uh uniqueness so there are two ways we could do this um one is let the database do it memory hey
Simon long time no see welcome yeah I mean writing documentation is hard again it's the it's the curse of expertise
which is why as in anything we do that is going to be consumed by others it helps to get feedback uh during in in the
process so that we somebody especially feedback from someone who's not familiar with the depending on your audience if
you're writing for like you should know this here I'm just telling you some details you should be able to to figure out
where that fits in the scheme of things um versus like something new uh where you're a novice and and and so it depends
on where you're aiming at not all documentation should be aimed at novices um it's it's actually kind of annoying when
there's documentation where it's like I know everything and you're like I want to know the specific thing about spring I
know spring like just tell me the thing um and you're going through like here's how to create a new project and here's
what the maven F like no just give me the thing um and there's certain there's a certain type of that does that it's
like let me start from scratch every single time it's like no I don't care I know how to set up a project no I know how
to go to the spring initializer I don't tell me how to do that don't show me the maven file just show me The annotation
and how it works uh so it really is I think the hardest part is figuring out what what your audience is who are you
talking to so so if we so as far as uniqueness doing it in the database or in in memory pros and cons I mean well I mean
Pro doing it in the database the pros are we're retrieving less data from the database um and it's likely going to be
pretty efficient it's certainly not going to be noticeable at least across the number of even if we had a million songs
I'd expect it to be pretty performant um and it will return less data uh less data is almost always better because the
in database processing is not where you're going to have performance it's serializing that data over whatever network
connection you have even if it's running on the same machine it's still transmitting stuff um what was I going to say
next uh so that the that's the pros the cons is um we got to figure out how to write the query because it's weird with
the un yeah welcome right down the street for me if that's the Cal I think it is yeah yeah and and so apis are
interesting like who is your audience how much do you of the domain do you have to explain to them how much of the the
data model that's implied and how much of the presumably they know how to how to call your API but even a but apis is
that's where it's like you want here's an example and here's another example and give me the if you're going to give me
Json give me the darn schema um it is so frustrating to hit an API and like okay and here's an example Json but it's
like two-thirds of what you could possibly get and so you end up with stuff like where this come from or what are the
all the possible values place um so what do we want to do do we want to figure out how think I'm leaning towards that
but what are you thinking um let's give it a shot out back to your screen so I think we can I think uh if anything we
can just try the um uh so we want to basically say I think we want um but let's change our test to to be what we expect
and then it so I think only money goes away right right we're just doing distinct yeah we should be changing the name of
this method over and over again but we are growing it so we're growing yeah um so you think just distinct at the end no
so it's going to be uh uh so I think astd is is basically where where I'm thinking um so select uh and then distinct
after the select ah and oops you lost the unest probably because you hit enter instead of tab or tab instead of enter
think I I don't know if that'll work I feel like uh what I've seen is we have distinct uh what quy language assignments
asks this is sequel we're writing in in the context of of a repository but this is all this is all sequ equal uh let's
try it at worst we'll get I mean we could if we really wanted to be sort of much more spiky experimental we could open
up a database connection directly and get a it yeah because what we won't see is we oh so now the ordering is different
uh oh wait it worked yeah oh I I I saw the zero and I thought we got zero elements so no it worked but it it worked
contains exactly as yeah currently so that's interesting so what order would we actually get we got heart first uh it
did money at the end the duplicate it did money at the end that's an interesting order um but that's fine uh uh because
eventually we want it sorted so um so we could say that this passed because we actually got the distinctness right uh
and now what we want uh so let's check it off uh we let's say I mean let's make the test pass we can say contains
exactly in any order and then we'll we'll basically remove that constraint or we remove that loosen what's the opposite
of a constraint because we basically loosened uh the constraint as opposed to to tightened it looser constraint looser I
guess okay so now we've got all unique yep commit yeah let's commit let's let's uh we got we got a new new new test okay
now sorting and now we want sorted so again we could sort this in memory but come on work so let's test Oh wrong one
this test okay so we I wonder if you select them all if you can ask intellig to sort them interesting um sure let me
undo it so there's sort sword content do it is that was it works yeah that's what we want oh I love intellig damn that's
good why should we have to do any work let the computer do the work wow yeah that all right uh let's drop the in any
order that's one of those things like unless you knew it was there or unless you knew to look for it like I must have
done it once in the past that's how how I thought it was there um like how would you know how would you know unless you
you I mean unless you're like me like like I I am definitely the type of person who will just read the documentation not
trying to solve any problem you know I think I was the kid who read the dictionary right just I'm just going to read the
I'm not looking for anything I'm just option all right uh so now now we can by I forget where do we put order by within
the I think it's at I think it's um so it's order by uh sending uh we have to specify what we want ordered so since we'
re just retrieving theme so it's theme uh ascending or just ASC yeah I think that's right uh it says ordering direction
is redundant um true but I I I kind of like explicit oh did somebody in chat say that uh no just saying I was saying
that because intell was saying that ah I see right here yeah no I prefer I'm with you I prefer explicit yeah running the
test fingers yep all right um honestly that was a little bit easier yeah but that's that's again like the the how how
fin slicing really helps you is is like just take it step little step okay drop down time y little more confetti hold um
should we rename our our test method and perhaps rename the finder method now that we've we've gotten it all where we
want it all things returned by find all for single song with multiple themes for single song uh well it's no longer
single song so with with find all for uh do you even need to say multiple songs I don't know that we need to say that
all themes yeah all themes return for all songs I think is all we need to say uh and then we can say uh all unique
themes return turn for all songs I don't think we need to say by find all okay so all themes all unique themes y
returned for all songs is that right that what I heard uh in alphabetical hey another nice uh so I think that's fine do
we want to rename now uh the all themes and make it a bit more explicit all unique themes sort of a sending we're sort
of alphabetically do we or is it just is that too chatty or you think name I I I feel like a little bit of of
explicitness would be nice so like all unique themes and then we don't necessarily have to say sorted we can do sorted
I'm just uh you want to refactor the base oh right so it gave you an option and I'm not sure what you selected let again
uh yeah shift F6 not yep you think that's good enough or you you're you were going back and could go either way um I
tend to write it explicit because when uh when you rely on Spring to to generate the sequel for you uh you tend to be
really explicit um I'm okay with that okay and you that's looks good to me okay done uh so I think that's it for any
cleanup yep okay all right so now we have a way uh of getting all our unique themes and in the right order so let's pop
back out now to so somewhere we have uh just below the HTTP level so our I guess it would be our our song theme Searcher
um somewhere we've got a test against that yep it's right here s all right um for uh what are our tests want you bring
one yep so here um we basically created one song and we expected that the model uh we actually aren't checking here
search returns model with no that's not what I wanted um think you meant this one oh no no it's this one down here yeah
yeah okay so what we want is if we do a blank search right that triggers uh the search page the the blank search page
and so uh what we want there is that when we get the attribute of themes um we should expect this because we created it
with with that um now is this test connected to the yes yesh I was going to say so so let's go look at at the
implementation because uh it may not be using what we think it's using which implementation of which method uh let's uh
no no of the um theme search that was weird ah so it does do it okay so in theory we run all tests it should work it and
it should be in that order yeah because that order is alphabetical already yeah I guess if we wanted to we could change
the order on the input online 63 uh well the L here it is out of order so oh so it it shows that the order did did
change yep all good cool um wait a second is it oh go yeah there there are no disabled tests left gotcha okay um that's
why I like I like the check mark yeah oh you like leaving the check Mark I do I I kind of like seeing all those all
those green things yeah there was a little bit of a dopamine hit there cool um yes let's sort in the or order of of
appearance in the year uh is New Year New Year's I guess New Year's Day is first yeah New Year's Eve New Year's Eve
would be last right so is that New Year's Day or New Year's Eve uh it says imprecise um all right so since uh since we
know that works and it actually retrieves the right model now um now we actually pop all the way out out out to the HTML
yeah actually do we have the HTML why do I do I not remember that I don't think we did it so let's go look at the the
HTML for the search page I'm just making one note um search page yep right okay so there is no there's there's nothing
just an input field um so what do we what do we want to start with we want to just start with a drop down in I think
that was the plan was to do drop down and then do into the multi- select right we all right work on tasks beyond that
yeah well we'll get this and then um so what we want then is to replace uh replace our our input here um we still want
the name to be requested theme uh but we want it to be chosen from the dropdown so we need to populate we need to create
a dropdown uh elements uh it is not called dropdown uh it is called select uh so select and then um uh since we're
pulling it from information in the model uh we'll want to do a th code curly shade themes or theme well what did we call
it I think we called it model this the yeah um so th field themes uh no that's not going to work because we let's see
are you doing some searching you want to share or no uh I'm just trying to figure out what we want so we want the name
to be requested theme but we want it to pull the content from uh we wanted to pull the content from the from the model
um so it be like a for each on and creating options based on for each well the select tag has has two parts so that's
what that's where uh that's where I'm getting confused um ah okay so here I'll quickly share my screen yeah so what we
want is uh basically here um so there there are two parts there's the I was right this is the field um and then the
options come from uh so basically it's one option per per item so we need that to be the the the basically the for Loop
to generate bunch of options so the select is the thing that gets sort of tied to the actual selection so right now we
have the input box with with the requested theme we want to select to be requested theme gotcha so so type would be
theme and all types would be themes plural yes so this will be themes this would be in the loop to expand on on on this
so basically this is connected to that right would we call that one theme yeah and that would be theme so and this oh
got it great because this is this is what gets connected to when you submit the form the name value pair this is
basically that name value pair so it'll take the the name of the field which is requested theme and take the selected
value which will be one of the one of the themes interesting that the example has the same name oh their examples are
terrible all right they're not terrible but they're not usually uh again again problem of not overly complicated
examples um as opposed to Progressive uh revealing of of of complexity um yeah oh this is by timely back uh so oh so so
let's do so select uh is that right requested theme singular yeah uh make sure to close the select each and I forgot the
syntax already uh um or here I'll just I'll just type it yeah uh so it's basically theme from uh and then from our model
themes uh and then we want th text to be theme I could spell it uh and then was there something else think that was it
oh th value yeah we assigned th um is that requested theme or um no I think it's actually also theme because this
becomes the um uh yeah so the text is what we display so sometimes you want a different value than what you're
displaying so if we were sort of assigning unique identifiers then we'd want the value to be the identifier and the
theme to be the text but for us we just want the want want the themes so I think that's want oops sorry I did that and I
didn't wow uh how did that get done interesting so I uh apparently you probably sent a keyboard yeah I sent a shortcut
that that didn't translate well into Windows got it got it so so what I wanted to do was that okay um and what happens
if you don't put the word theme there on line 6 that's just for preview so that doesn't that doesn't that gets right so
that's one of the nice things about the time leave templates being these this idea of a natural template is you could
preview it if you hover over in the right you could click that and we'd basically see a drop down with theme in it right
um if we didn't if we didn't put theme there then the dropdown would be empty I'm not sure what it would do um right and
now we get rid of this uh yes and we get rid y just to select welcome uh welcome welcome uh so there's a question back
here uh do we have a limit on my on our search um no we're basically returning all all unique themes uh the expectation
is be all that many that we expect a problem uh we will not want to fill all of them into a dropdown that's just the
autocomplete so uh I wonder if question was about yeah I was one of s's question was about um you know exposing leaving
things open for um SQL injection but that's not really an issue because we're doing it through yeah I mean we we might
want to to do limits in paging once we get to the results um right but even there again we're not talk our our our data
at least initially is is not not that large but we'll we'll um just looking to see if there's any other questions yeah
so there is is um for the songs there's also sort of some ranking that we might want to do uh and who knows maybe we'll
bring in a vector search uh since it's so easy to do with with the libraries these days um we'll see so Vector search uh
is is a way of saying um this song matches in a sense this song has more themes that you're looking for and so maybe
that's useful um you know than this other song that happens to match one but this one matches two so maybe that's more
useful and should be ranked higher uh but um well we're answering questions uh X proof asks how do you document whether
or not field can be null in your projects um field of what you're gon have to be more precise than just field well since
uh that's not quite a self-limiting data set for for a radio station although I don't know how many how many songs like
how does a radio station acquire new do they get sent stuff how does that work so we still get sent stuff it's a
combination of physical and digital um digital is actually still a problem because um most College Community Stations
don't have a good there's no good software for having a digital library right right and we talked about this a little
bit the broadcast stuff is you know top 40 radio doesn't have that many songs to deal with um so for our kind of radio
like our physical collection is over 120,000 items wow physical pieces of music yikes um where is it all it's literally
right next to the DJ booth oh wow okay yeah um yeah maybe I have a see yeah so I mean you You' yeah you you you want a
system that is dedicated and and can handle that kind of volume yeah do you still have records I assume you still have
records oh yeah like there we go right there's a view of the library the back wall you can see it's go away on the back
wall you can see is those are CD shelves right and they wrap around the room right y that's a lot of stuff yeah it
doesn't even count the the thing we call the Behemoth uhuh which is on the extreme right you can't really tell where
well you can sort of tell this line here yeah see how it goes through the word BL poster so that is a large cabinet that
is like these wooden CD shelves at the end of this aisle except there's 16 of them and they're drawers that oh right
okay okay like this and that alone holds uh I think it's 60,000 CDs in jewel boxes oh wow yeah and we're getting rid of
jewel boxes we're moving to sleev yeah I was going to say jewel boxes I I know in my collection I got rid of rid of the
they're thick and they're brittle yeah they're always cracking and and breaking open and yeah and it just seems like
such a waste of plastic yeah and they're not recyclable as far as I know yeah well plastic isn't really re that's a
different rant um 120,000 row HTML table Yeah browser might have a little bit of difficulty with that but that's only
albums not songs right exactly multiply that by roughly eight eight yeah so yeah um so X proof uh how do you document
whether or not method parameters and Constructor parameters can be null so again what types of objects are these domain
objects are these dto are these something else although it's pretty much either one or the other um domain objects
should just be never you should just never hand in null period end of story um and then the way you document uh uh that
is use annotations so there's not null there's null um those annotations are useful and their use usefulness will will
expand if J specify ever gets off the ground uh then that will be um I don't think we use those in our I thought we did
I thought we did two but no no no is I was like I thought so intellig will sometimes generate that for you yeah it
generates it for us we yeah we haven't I don't think we've explicitly done it anywhere no so uh I would use annotations
to to document that uh an exper asks if you use hexagonal architecture if you wanted to switch off Spring boot would you
be able to that is the enti one of the I wouldn't say top benefits because it's pretty rare you switch Frameworks but it
does happen especially if something lasts over five years you're going to want to at least be able to switch Frameworks
um I think I've done that twice in my career to take something that was non-trivial and move it to a different framework
um but yeah because everything inside your hexagon has nothing to do with the framework uh so basically you just just uh
you'd have to replace all your adapters but presumably the value if it's a very it's a if it's a fairly domain Centric
application the value is inside the hexagon and stuff outside of it is just yeah I mean even and and we've talked about
this on on the stream before I generally just do not want nulls in my domain period end of story because as and I think
we did this last or I talked about this recently where it's like null means something and so make it explicit what that
meaning is if it means it hasn't been filled in yet have some way to indicate that so it's obvious and not just null and
we don't know what that means yeah so I think one of the one of the bigger benefits um is uh for example being able to
switch one of your adapters from uh one mechanism to another so maybe from uh a request response you know single page
application front end using Json over HTTP apis and you decide too complicated we just want to go and use the web as it
should be uh with some HDMX on the front end uh then you just then you swap out the adapter um and everything else
pretty much remains as is um and I guess technically it would be you would add an adapter and then eventually get rid of
the other one right right and the beauty of it is that the because the adapters don't talk to each other and are
independent yes you can rip out an adapter and nothing else should suffer which to me is one of the yeah you've got your
thin vertical slice that when you remove it it's totally clean yeah all right um should we break before we do the next
step uh I was when we start was it an hour ago yeah it was an hour ago okay um let's uh yeah let's keep people suspense
not um all right so we'll take our our coffee break uh and when we come back we'll look to see if this works so stay
tuned for that and enjoy enjoy the n so uh little commercial break uh after your coffee um as you may know I have uh a
board game called Jitter teds tdd game and folks love it uh and you can buy your own copy if you go to td. cards uh but
not only that as you may know if you're uh paying attention to my streaming uh I am creating the online version of the
game because it's a physical game which means you have to be in the same place uh you can also host it uh which is
something I've done but uh it's not as easy as being in the same place and certainly not as fun but since lots of folks
are remote um working on an online version and so if you purchase the physical copy you'll get Early Access uh to the
online version when it's ready um probably towards the the end of the summer is my uh at least Le some are here uh is is
my guess when when it'll be done I also wanted to mention uh uh that um I run a book club um and so every week we meet
and talk about a book uh we meet on zoom on Sundays and you can find out more about that uh by going to Ted dodev book
club um we are in the process of selecting our next book uh and uh in fact the polls close tomorrow so once we select
our book we'll uh folks will get a copy and read the beginning of it and our first discussion is likely gonna be on uh
in a few weeks on June 23rd I got the date wrong last time and so uh it's open to anyone who who uh wants to join even
if you can make all of the sessions uh I encourage you to join anyway and and drop in um if you don't care which book we
select then you can just hang hang back and wait uh until I announce it which will be on Thursday uh and then uh you can
you can join in if you're already in the Discord then just make sure you send me a direct message to be added to the
private channel for the book club if you're not just go to this page uh ted. dbook club and uh you'll find a link to the
Discord uh as well as some other information about it and so that's coding uh so let's see um just some comments yeah
future from soap wisle my gosh soap wisle I saw um there was a survey that came out from uh the spring folks talking
about sort of what people are using and so on and and soap soap came out as still being used but like by some 50 some
perc and I'm like wow that's yourself there we go I was saying I've certainly worked in those kind of Enterprise gigs
where they're um hesitant to move to a newer technology yeah there's um there's a certain uh so charity Majors who's I
think is still the CEO of of honeycomb um she I follow her on on the various social media and uh related to to some of
the stuff she talks about is this idea of always be migrating um and so if you are used to and your and your software is
set up and designed to to be easy to migrate and migrate is not just the database right so you may do database migration
so getting good at that is going to help you um again this is sort of all under the to me all falls under the the banner
of if it hurts do it more often um because then you'll get you'll get better at it and you may find ways to uh to
automate it and reduce mistakes and things like that uh because invariably things you do less frequently uh are the ones
that cause you problems um so always be migrating always be sort of ready to to adopt new technologies even if it's just
like you were saying before Mike like keep the old adapter around create a new adapter try it out see how it works can
you do that like can you do that in the first place um if you can and you try and you try out different things then you'
ll be much better off when you actually then do have to change another yeah and especially um you may not change the
framework I guess brand is is what I'll refer to it as like you may not change spring but you got to migrate from 1.5 to
2.3 to 2.7 to 3.1 to 3.3 and migrate your Javas along the way um the more you do that the more frequently you do that
the better at it you get and and then it just when you are then forced to upgrade because oh my God there's a huge uh
security cve thing um you're just like okay we got it we're done deployed just like another day uh as opposed to a big
fire crisis everybody running around trying to figure out how to deploy because they months and yeah and presumably if
you're good at that you probably have a good set of tests um which makes it then easy to to try out the next version of
the library oh that doesn't work that causes this problem um or everything is fine and you deploy confident that
everything works works Basic I gotta say I I I really miss Visual Basic there are parts of it I don't miss um but I
really miss the the the environment that was that was just so great all right uh do we want to see see what happened app
and actually I've heard to do this off screen because I need to do the actually shouldn't do that until it's up and
running okay now it's up and running is it still called theme search as we'll find out no it's called theme no no no no
you got an error uh parsing so you can either look there or you can look in the uh in the IDE but somewhere we we
probably messed up something uh you want to switch to the ID n it's fine basically be name requested theme um so
requested theme we didn't mark as as a bean uh so let's uh let's go look at our our controller we did something wrong so
let's look atong song theme so boy that's a tongue twister song theme Searcher there you go uh so we just have it as a
request pram it's not actually a bean uh so that's fine let's go to the HTML we'll so this so the reason why uh you
might want to do it this way is if you have something in the model that says here's the requested theme kind of that you
already have right so if you were on some like you know where it was pre-selected for you because previously you had
selected it but that's not the case here here we pretty much start from scratch so I I think if we just change it to uh
name equals I think it's basically get rid of this and just say theme I think it's name let me double check without the
curries yeah without the curries because we're basically saying we don't need you to uh again uh you shouldn't have to
so if you do um if you click on the already stopped it so oh you already stopped it okay so you shouldn't have when you'
re if you're just changing the HTML you don't have to um what you do is uh you you you basically give it a little kick
by doing a a build a rebuild of the current file which technically makes no sense um but if you here let me show you in
the menu if you go to uh build and you basically say recompile this HTML file which on the face of it makes no sense but
what that does is it refreshes the the cache uh that the server the server has got it okay going to grab hyphen okay
inspect and we'll probably see that the the form options are empty is my guess so you can we can open this up yeah so
our select is empty that's fine that's that's okay we'll we'll figure it out let's go let's uh where's the connection to
the model again so line 13 should be the connection to the model it should be model so let's go look at the controller
Searcher uh do we have any songs in the database are we pre-loading anything uh don't no so there there may not be
actually any themes so let's go to the import is it called bulk import no song import now you have to off now I have to
go off yeah pardon me pardon me while I go off screen yeah um good old on eror resume next for those of you who remember
and that and and that goes way back before Visual Basic uh so I uh I wrote a basic yeah stuff is there's too much going
on interesting I've got a going on forbidden yeah is it still search input oh song input no remember we put it under
contributor ah yes yes so what you might want to do is is get autocomplete okay off screen or on screen uh well you're
already logged in right yeah yeah so we can do that so if you um so you should be able to and then we don't want to see
this anymore so we can hit the X here and then the same with this one uh and then the same with this one and then
basically erase this and we want that one oh there it is that one yep okay let me get some yep uh so as ask why is the
name is requested theme because that's the when the form gets submitted it's going to be the name value pair or pairs um
in this pair because it's a single select uh so requested themes the name of the query parameter that it should submit
Okay so we've got a variety of themes there all right so now we know which we should we should see roughly welcome just
so we can reference it if yeah did you refresh the page uh I did an refresh uh okay we are are so now now I'm wondering
if we've configured the app correctly right yeah okay where to uh so let's go to our configurator which is in our song
themes startup sorry Thong Song themes config uh anything it's always configuration it's so we want to um get rid of
that completely that meaning what your cursor is on just delete the implementation oh this is the old implantation yeah
no no you want to leave the method because we need to uh we uh let's search for before you do that let's search for
implementations of this of the class um I know what the keystroke is on on the on the Mac let me see impation of in so
Control Alt Control Alt B so click Control Alt B there so that shows the implementations of that interface uh so let's
go to the jdbc theme finder that didn't go to it you went to the wrong one I you went to the and go go back to I mean
you can do it from here but I want that to sort of here B so it's like control B with a modifier of alt show show so you
hit entered you went to the anonymous implementation you want to go go down oh yes yeah the color coding messed me up I
thought yeah that was selected it was this one got it um so this implements theme finder this is in the jdbc uh will it
just find it it might but all you need is a method name though different because isn't the um don't we call it back
there it's called unique oh maybe it is yeah did a rename and it went all the way through yeah so actually you can
delete the this Bean thing entirely because we it'll use um what what spring will do is it'll say uh uh in the JBC theme
finder since it's a bean um and so we basically look at it but basically it recognizes it as a bean and it implements uh
theme finder so it is a can it should be a candidate for injection into where where we need it um so let's again so that
run button becomes a restart button so you don't have to manually stop it it will just restart it ah saes saved you a
click yep well next yeah okay we're up and go again probably although you could that and here's for reference yep oh
actually I will not show at the same will so should we select Halloween and expect three songs back I think it's four or
t-shirt uh one two three oh it's four yes it is four I Halloween oh there's other dat data in there's a bunch of
duplicates oh right because we running dumping over and over again yes yes because when we thought when we thought there
wasn't data in the database it was the select wasn't wasn't wasn't reading from the database let's do do a t-shirt is
only one so that should give us one for each import we did right yeah there it is so yay yay cool all right so I think
we y what uh I mean we could you know drop the database and and and start again but mean but we we'll figure out how to
how to deal with that but we can check off uh implement the drop down y we have implemented the drop down and now this
is done yep now we can sketch out next well let's commit and then we'll um right okay so let's yeah so our goal time
yeah Parker time they're all ones um uh so looks like we sketched out some next steps uh there's sort of the words yeah
uh Still Single theme but it will autocomplete as opposed to having to look through a long drop down um oh why do we
have failing tests oh all my guess is because that we removed yeah that's that's my guess is there's one of the my brain
did at that point go hey maybe we should rerun all the test yeah and then I got distracted by some bright shiny object H
Lord knows what but yeah I figured it was the MVC tests yeah yeah they're just not set up to have the um they're
probably just missing the the reference to the uh to that theme finder Bean that's fine we can go look at those you want
to fix that now and then we'll yeah let's fix that should be pretty fix uh so let's scroll the way to the top so we can
look at the annotations on the class uh so import song themes um now deleting that being made the regular drop down work
so we can't put that being back well none of these method te none of these tests care about the contents of the
repository so I think we can just add um another mock Bean which basically says create one that does nothing so let's do
that got to give me a little bit more instructions yeah so here oh mock Bean like there yeah so just another mock finder
yeah and let's just run yeah let's just yeah works okay so let's run all that just to well we got to fix the other MVC
one because it has the same issue so you can copy copy and paste that so it's a reminder for folks who are not too
familiar with spring um because it's a web MVC test and we could probably even be more specific and say we only but I
think there's only one controller anyway this is what's called a slice test which means it does not do component
scanning so it won't automatically pick up the theme finder that we have um unless we're explicit about it in some way
and so uh we do pull in the song themes config but now we no longer Define theme finder in there uh so we have to then
explicitly uh tell it to create a theme finder that can be injected into the the controllers and the advantage of the
web um we just scroll back up get the name of that web the webc test is that it doesn't spend as much time scanning and
pulling in right all of God's creation basically yeah so it's faster right that's and that's that's yeah it's much
faster because it as you said it's like it doesn't have to scan it in fact it does no scanning um pretty much uh it must
do some scanning because the web MVC does pick up those annotated with controller or rest controller um but it doesn't
instantiate everything that's the thing that takes time um so uh that's why you what you can do is you could pass a
parameter to web MVC test oops sorry oops I clicked there I was typing in the middle of in another window sorry uh so
web MVC test does take a parameter just like you know the import does and you can basically put say here um which
controller do you want to explicitly UT Port uh we only have one controller so it sort of doesn't matter but what's nice
is is uh I mean if you want you can actually do it and just say uh song class and so that way when it starts up it will
only instantiate that specific controller and so if you have a bunch of controllers this can also save you time because
it doesn't have to instantiate 25 controll ERS and so these are slice tests because it's like you only need these things
sort of the minimum amount of stuff gets instantiated for you uh through uh instantiation and this is why you know if
you're going to write spring spring based tests you want to slice them up as much as possible so that they do take less
time to to run so let's go to the other MVC test I don't remember which one it was do you I don't remember either uh so
we can just run all the MV just not all of them just yeah uh yes Simon that's exactly right so it's pretty much um I
don't like the word integration test I call it a framework test uh so it uses the framework the framework gives it a a
mock HTTP server um so we can test things like does the routing work uh and then um so it's not running a real web
server but it's but it's instantiated everything else that it MVC yeah so same thing um it's just oh yeah pretty much
for for dependency injection I mean the term is is is always confuses me because uh or it doesn't confuse me but but it
can make it difficult it's like what are you referring to because there's dependency injection which to me is pass
parameters into Constructors pass dependencies into Constructors and the word injection is a fancy way for saying
passive parameter um so there's dependency injection which is pass dependencies as parameters into Constructors uh then
there's automatic dependency injection which requires a container and that's what spring does with auto wiring um so I
love dependency injection how else are you going to make things testable whether I like automatic dependency issue uh
what happened these um well our test passed the one we just fixed um but we've got some errors 404 here did we import
the right uh we may have not imported the we did the song theme secher but this is the Importer we imported the wrong
MBC class oh that was my fault I I for some reason I thought there was only one controller we actually have two
controllers so let's do this right um let's go back up to the MV web MVC test annotation and specify the not song theme
Searcher so and so that why that and so this shows what happens when you do that is it only instantiated the controller
we specified and so therefore it was a 404 because what what are you talking about we don't that there we go there we go
so for the other one uh so for the other MVC test the song themes MVC test uh we can specify that one is the guess I
think we only have the two controllers right yeah import and theme Searcher yep y uh fr the back L the browser here on
one side M uh yeah so so the mack MVC um you can actually tell if you want so for example if you somehow think you need
a real web server and maybe there's some reasons that you want to do that um you can actually pass a parameter to say
random Port blah blah blah uh and then spring will actually create the embedded web server um either Jetty or nety I
don't know what it uses by default now um and then you will have an actual real web server uh so that takes a little bit
longer because now it actually has to run the embedded web server but for certain things it might be what you need
especially if you're going to be running um something like playright or selenium or something like that that actually
does need uh a real web server to to test against um I think those test might be useful uh slow yeah so there's there's
some things around uh what's what's called uh application context caching so there's some caching that uh spring does so
that it does not have to for every test and there is some some way that it does the caching based on what actually gets
created per class so um I honestly have not fully gred what what it does enough to to figure out how to how to optimize
this stuff um but there are ways where you can say look just create everything you need for all these tests and then
then you're done for for all these tests and that would be the the most efficient but we honestly have like four tests
so I'm not I'm not too wor about optimization but it definitely on any non-trivial project you're going to want to
figure out how the application context test caching Works um because otherwise your tests are running slower than
necessary and doing more work than do all right so now that we've got a clean slate um sketch out yeah so uh uh I guess
we want to do what that one says um so we want start typing so basically single selection saying um do we want to sketch
up further than that yeah I'm wondering if sketch below yeah just just move that up yeah they can is it just descriptive
text or do you think it needs to be a box I think that's just describing it in yeah uh we actually kind of did 21 as
part of implement the dropdown so that detail we don't we don't need right unless you want both of these can go yeah I
think both of those can go I think we did oh I see what you're saying this could go here yeah beforehand all right so
this this is gonna be fun look at that we're actually at the point where we're we're finally going to use HTM X yeah um
so this will this will be fun um so I think let's see so let's think about this uh what we want is we want an input
field so why why don't we uh bring up the HTML because we're going to sketch there and then let's let's maximize that
yeah so let's put this above the the drop down um we'll keep the drop down there just so so we have it um so we're going
to want an input field that's that's of type text um uh we want um are we going to use that Library we talked about yes
we're going to use HTM X yeah so uh oh I was thinking something else what was that oh that's the UI Library we're not
we're not there yet um um because that didn't provide the um that doesn't provide so so there two there there's kind of
two ways to do this one is you load all of the themes into the browser and then let it autocomplete from there um that's
great if you've got 10 20 30 50 if you've got 100 200 300 you're basically pulling in a lot of data that uh is just not
a good idea um I mean we we could do that but I think that's that's not a good design um so what we're going to want to
do is every is so so high level is when you start typing um based on some delay uh we're going to basically in you know
so if you stop typing for half a second it's going to call a method on the server saying give me all the themes that
match this these letters so if you type h and you wait and hang out it's going to do a query saying find me all themes
that start with h and so it's going to return honesty and Halloween and and whatever um and then as you continue typing
it will do another search uh and then at some point you'll you'll hit enter and that will be basically fill in the the
auto complete uh fill in the text field so because we got a bunch of modifiers that we're going to want to add there um
so what I like to do is put the line oh this closing bracket okay yeah got it uh so then on on next line autocomplete
equals off because we don't how does the browser autocomplete off work is it coming off of a list that it's already in
the H yeah it's yes well it's it's it's what whatever the browser thinks it should autocomplete for that field and
usually keys off the name of the field uh which reminds me then let's give this field a equals uh theme not what's going
to be submitted for the actual theme search this is the query for autocomplete so the results of searching here will go
into uh another drop down um so we got the name we've got the autocomplete off uh let's do um uh HX trigger so HX D HX
DT trigger oh so what this does uh is basically tell HTM X which we'll have to go up and and equals um input colon yeah
space and then delay colon 500 Ms it seems actually long to me but okay yeah it's it's basically a bunch of things that
that we're we're telling HTM X hey when the in 500 milliseconds oh 500 milliseconds is too uh we could always adjust
that yeah um we can try have a second yeah which you don't want to do is is if it's too small then it starts
autocompleting like while you're still typing so we want to allow for for some amount of typing um yes I think we'll
need the closing tag to be a slash self closing tag we'll fix that and good night asid have a have a good evening right
rest of your day I guess rest of your night uh no no you wanted self closing so basically just gotcha slash before the
close yeah yeah um we want to put after the 500 Ms comma do you want to share what you're looking um I'm just trying to
look at the the type equals search uh so I'm basically keying off of this example from from uh from HTM X um so we have
uh is it the SL search yeah so it says the search trigger will be run when the field is cleared uh we specify another
trigger to search so unclear what what trigger does let's are so we did the delay we said how when um this is a separate
event that will trigger this whole thing so what this trigger says is when the input changed after and basically has not
and sort of has has settled for 500 milliseconds it will trigger this event the post and then the post the result
results of that uh go wherever the target says which is basically search results down here and so we want to do
something similar which is when the input changed we we wanted the HX post which will in a sense run the query we want
the response of those um to to show up uh what we'll wanted to show up as as basically what looks like a drop down
underneath the input field um this search refers to this search so I guess there's a type of element input element that
is a search um so when you hit enter on the field it it does a search uh but I don't think we need that right now
because I think just so you can sort of force the search by by by hitting enter um but we have the the change DeLay So
that that'll be enough for for I think that what we want to think about is what's the minimal thing that we want what we
want is if you start typing and you wait half a second it should invoke post and we should and we just we'll just
display the content somewhere so that'll be our sort of minimal uh sort of a minimal Spike we're sort of spiking here a
bit so we're not going to be test testing this all right so let's see if we can get that get comma then yeah so we don't
need the comma so so basically HX trigger is basically a set of events that will cause whatever the in a sense action is
on on this field um so let's so that's our trigger we want it to post and uh what's that endpoint going to be uh we don'
t have an endpoint for that we'll have to create one um so what do we want to call that endpoint this is the endpoint
where we'll do a post with what's currently in the input say we could just put it against themes as an stra themes yeah
like that sure why not we don't have that endpoint what was the shortcut to see all the end points it was a cool uh if
you click if you click on Spring down here ah and uh I think type controller uh so select NBC so it shows there's a way
to just click here and then Bean graph or maybe not maybe I have to select on each one so that's slash that's
contributing and that's theme search so themes is probably fine there is a way to find all of them and and yeah and I
only seem to come I only seem to come up with it accidentally I never know how to like intentionally get it there I just
don't use it a lot so it's not something I've I've yeah let me check my notes because I think we did it last week right
and so I know we did it before yeah yeah um I made note of it uh so Simon yeah HTM X is is a small frontend JavaScript
library that makes it uh so we can do the kinds of things we're doing basically Ajax like stuff um as they used to call
it uh with just in a sense data parameters or or new attributes on existing HTML elements um it doesn't uh so it's just
JavaScript that that basically does this does this for you so so like we're we're saying here with the HX trigger it's
monitoring and when the input changed um and there's a half a suck between the last key you pressed it will go invoke
the HX post for you take the results and and put them basically to so it's not spring specific it's it's Library Yeah so
basically it's it's you know why should we have forms for everything uh this will actually be sort of post posting
itself uh and we actually won't need uh we might still have the form but slash oh so it does come up in in the in the
all search H interesting well no I did control shift slash right but if you see that that's actually the this is your
standard search menu right yeah yeah so you could I think if you just come into it normally like if I did control shift
n oh I guess it it's still there yeah so it's there ah but there is a way to get it to to appear down here down there
and I don't remember how to do it I'll have to look that up uh oh there it is it's over here it's in a separate separate
thing thanks J I was typing in other window so there it is I don't know why that I don't know like I there's a lot of
things that that the ultimate addition of intellig idea does for to support Spring um but some of these tool windows I I
don't I find like why is this a separate tool window why isn't this part of this the spring tool window I don't get it
anyway um so we decided on themes as we decided on themes um do an import H uh yeah we need one more thing and then
we'll do the import um so we need to do a target for the results so we'll Target um and let's target uh no so the target
here is a an ID or a class in the HTML in the in the Dom ah uh so we're going to make one so let's do um Octor no I'm
kidding hash uh hash and results and so on line 20 let's create that and we'll just create a yeah we'll results huh
interesting it's not autoc comp completing it because it doesn't know that it ex it's it doesn't know about it just
because we did it right right right right it would autocomplete if you now tried to reference it from line 18 right uh
but it doesn't it doesn't clearly way or it doesn't know at all all right it may not because it may not recognize the HX
Target as as a as an attribute right right speaking of speaking of um let's uh so let's go grab it uh where the heck is
it we'll want it to grab it from the CDN is let's I feel like you pasted before yes I just up let's see oh I'm I got it
oh do I need to turn that on no it's not in it's not in my uh clipboard or it's not in the uh so un undo that clipboard
yeah that's something I need to do yeah I'm not sure how to how to do the clip how to how to share the clipboard person
private chat yeah I'll put it in there or regular chat I'll just put in regular chat no I'll put in private chat because
it's got some special stuff yeah so grab that and put that in line uh not in line four sorry that's not even the right
place yeah uh it'll half so now I'm curious now it's so so just because we we imported script you'll notice that that
intell has highlighted these HX things because it doesn't um there there is probably a way to set up a name space for it
but um I just ignore um yes there is an htx plugin uh last I tried it it wasn't all that helpful I updated uh so what we
want to do um let's test drive uh well let's let's take a break because it's another been another hour um when we come
back from the break we'll test drive this endpoint just to return some some data directly and what we'll do is then use
that to to basically test this to see when we type does it return right the it'll ignore what we send in as the query
it'll just return values what we're what we're going to check is basically does it um does the UI do its thing does the
UI do do what we expect it to do yeah yeah all right we'll take a break and then we'll we'll go ahead and and test drive
that new endpoint so stay n uh so just a a reminder to folks who didn't know um I am not only a streamer but I'm also a
technical coach and trainer and so if your team or even you as an individual need some technical coaching maybe you want
to learn tdd or perhap perhaps you want to get better at refactoring or design um you can go ahead and go to ted. deev
and go to the about page and you can find out how to contact me or you can just send an email to Ted ted. deev uh and we
can be happy to chat for for half an hour and discuss what your needs might be um if you don't need it uh maybe you know
somebody who does uh so I not only help teams in in organizations get better at refactoring and testing basically all
the stuff you see me do on on the stream uh and I also help individuals who might want to just improve on on their own
so uh you can contact me on the Discord or or via email and happy to set up a short uh right uh so so we want to write
our that uh you're sound is a little that's why there we go that helps yeah it's funny how microphone placement makes a
difference yeah funny that yeah yeah weird so uh where do we want to put it do we want to put it in song theme Searcher
gonna uh what do we have yes probably s theme Searcher since it already has access to the the dependency that we're
going to use which is the theme finder so that's probably a good place to put it yeah we got to use the endpoint toolbar
y yeah so we're using it there on line 27 so we should probably put it in the same in the same place um we could pull it
out into a separate thing uh I think we we might want to look at at that um going as a refactoring uh but for now we'll
just stick it here um but we want to test drive it right so I know it's so it's so tempting let me just go ahead and add
in this this endpoint here uh since this is a new endpoint we want to start with the MVC test oh right go and we're
going to basically want a test that uh does a post to the endpoint and it should return in this case it should return a
either is it Danny Penny or Dan pan how do let me know how you want to pronounce it um it's a good question Dane pay D
any any one of the above um it's a good question though how do you tdd for void methods um basically you uh generally
void methods methods that don't return anything are likely some kind of command so they're going to be it's some kind of
request to change State somewhere um and so how you test that in fact almost all tests are testing a void method with
the the requirement that you have some way of observing that change so if you look at our you know these tests are are
sort of framework tests so they don't really count but if we look at some of our other tests you want to bring up a
random test yeah so here um this is still at at the framework level let's bring up a test that's not application yeah
this might not be good either because we don't have much behavior on a song yeah let's look at application test that's
right searching for an empty string now in the result let's scroll bit Yeah so these are these were're here we're not
testing commands directly these are these are all things that return stuff um test yeah so these are these are these are
actually none of these are are commands so we may not have a a great example of that so um so generally what you're
going to do is is pretty much you you set up your test you execute that command which is going to be a void method uh
and then you're going to do a query uh to something has to tell you that the state has changed so the state started at
this point you ran you executed the command and the state in some way changed and has to be observable if it's not
observable that I can you know then how do you you know what is the what is the command doing and sometimes this can be
tricky if for example the only thing that that happens is you write stuff to a database um well then in your test you
have to read back from the database and see okay that that's now in the database but what if it's just that you sent out
information to a third party service this is where most people uh for better for worse mostly for Worse would use
something like makito and add a spy or or a mock and detect that that the thing was called there there are better
techniques than that um still using the idea of a test double of of like a spy um but I think there are better ways to
spy than than using makito because makito uh leads to very um code that's just hard to understand and slow to run uh but
you basically are substituting what Gerard mazaro in his book xunit test patterns calls indirect outputs right so I
basically say Hey you know I'm playing a game of blackjack I got a card dealt and we want to send off information to a
third party service how do I know it did it is I'd have to substitute the real thing with something that I can then
observe oh look a message came through saying um this player uh got this got this card and so it's this indirect output
that test doubles are really what what you want and so you're going to need some way of of in a sense tapping into what
would have been sent out by your code to this external thing uh did it the thing that we expected so my preference these
days is to use James Shore's output tracker technique um one of the things you you'll find if you watch my uh tdd game
streams is uh since we're already generating events in the domain so if you're using something like event sourcing or
domain events you can just tap into those did this domain event get generated and just tap into wherever that that would
have gotten sent and so it it applies in in no matter sort of what you're doing uh you're always tapping into uh
replacing the real connection the concrete thing that's talking to some external service and you're replacing it with
something that in memory you can ask what messages got sent what information would have would have would have gotten
sent um and uh especially if you're using something like DDD plus hexagonal architecture um makes it really easy because
you just replace your concrete adapter with with double um so I don't avoid mocking so mocking is a term that is
confusing because what do you mean by mocking uh sometimes people when they say mocking they mean using the tool mockito
and say and write the word mock in their code that is a form of mocking using a tool that I do not like um so I avoid
makito unless I'm in a situation where I don't have a choice Legacy code is sometimes like that but mocking itself um
the term I prefer is using test doubles so the idea is replace a real thing something that tests against IO and
replacing it with something that I can verify in memory um so mocking doesn't indicate a so test doubling is not a
indicating of a bad design it's indicating actually of a good design if I can play something with something else and be
assured that it did the right thing that it interacted with this external thing correctly um then then that's actually
what you want and a lot of times you're not going to need to create um what is technically called a mock which is a
self-verifying spy um a fine do you have a particular um previous stream video that as you go through test doubles and
yeah so funny you should mention that so I've got a video on hexagonal architecture and I go through test doubles uh and
how that works and and what the code looks like uh and what the tests look like in in that scenario um so if you check
out J.T uh and look look for hexagonal architecture uh you'll find it um I also have h a course that I promised folks I
will be reopening uh which is refacing to testable hexagonal architecture um month and I have a bunch of not just a so
one of them is a presentation basically an hour or so presentation on hexagonal refactoring to hexagonal architecture um
but I have a bunch of videos where I basically go through that uh if you're interested in sort of longer form stuff a
bunch of streams that have recorded um that that talk about that and of course we're using hexagonal here and uh I use
it in on my stream uh so there's no shortage of if you're if you got time to of videos to watch uh for for that and yes
as as uh Jonas did uh I also have a Discord where we have an entire Channel dedicated to to this kind of stuff actually
several channels on testing and hexagonal testable that all right so uh do we have our endpoint test yeah where were we
we were doing that in we were going to do it in song theme Searcher test right did we write it yet or we were just
starting to when we went I think you were just you had just generated the test method an empty test yeah what was that
oh wasc NBC test yes there we go okay and we were testing posting yes posting to that endpoint we just defined which was
themes y okay I have to I have to rant a little bit okay clean architecture is not hexagonal architecture hexagonal
architecture is not clean architecture despite what our Dallas says Where oh who cares it doesn't matter it matters
words matter definitions matter and clean architecture and hexagon architecture are not the same thing they're very
similar but they use different terminology uh clean is for whatever reason very popular in inet it seems to be the
dominant uh architecture other than vertical slice um I don't know why that is uh hexagonal was there first um uh the
main difference is um clean subdivides things into the M an application layer which I uh am in favor of uh what I don't
think clean does as good a job as is focusing on inbound and outbound adapters um but hexagonal and clean are similar
just like onion is similar and all of these testable architectures are similar because they're all trying to do the same
thing is is is separate IO from from from your core domain um hexagonal explicit as Alister uh Coburn emphasized in in
his book uh that just came out um he does not separate a application layer from the from some domain layer so what I'm
doing is is not hexagonal uh I do and and I'm actually starting to to stop calling it hexagonal because um it is what I
do is not hexagonal uh but I I just had to say that because this is how semantic diffusion happens is because people
stop caring about using words precisely and it really upsets me because it means that now it's harder for for people to
communicate this is what's happened with with other terms and it takes no effort to use the right terms and so I'm kind
of annoyed at people who's like ah it doesn't matter it's like it does matter because now I can't talk to you and you
can't understand me uh because we're using the same words then now they mean different things um so sorry I had to had
to had to rant about that so basically I I call it the DDD plus hex uh architecture because it's it is hexagonal
influenced um definitely and I like the shape of hexagonal um but uh it's clear aliser and I differ on um the need for
having a separate domain layer from from application so all right Ted Ted Ted GLE no tagon I mean basically I put it on
I so often when I talk about these days I I just talk about testable architecture uh in fact I have a course I'll be
renaming my course to that and I I think it's really I think it actually is is is extremely helpful to separate the
domain layer from the application layer um I I don't want to go too deep into it right now but basically if you have a
DDD if you have enough domain it's worth it to have a separate layer because then that layer can be completely ignorant
of IO and you therefore will never use test doubles in your domain layer uh because there's it's not even aware that IO
exists Hardware doesn't exist it's just running in Ram that's all that's its entire universe um and I think that's
helpful yeah this is all sorts of stuff around vertical slice and I think some of these are are are compatible with each
other you can do vertical slice plus clean plus plus hexagonal plus domain driven I think you can you can do them all
it's a matter of um some of it's a matter of how do you organize your code which is very different in net Java so uh all
right so let's get back to doing our post um so we want to post to endpoint and let's there ah here we go yep and then
we'll and expect yep y uh I think here we want to be very precise we don't want to accept any just General um successful
here I think we okay um all right so if we run this what do we expect well the end point doesn't even exist so what
happens when the endpoint doesn't exist um uh we got a 404 404 okay yeah yeah all right so let's uh let's run we can
just run this test class I'm gonna stop the server it's been running for a while oh no you really wanted to uh give it a
break you should just run yeah yeah that's that's sort of the sense I get since um it's really it's really interesting
um and I'm not sure if it's just sort of the bubble I've fallen into because of of social media reinforcing certain
things but it seems like the only people talking about testable architectures like clean and mostly clean um or net
folks I don't see I see very few at least on social media Java folks talking about any kind of testable architecture
whether it's hexagonal or clean um there's just not as much chatter whereas I can probably name five people who I follow
who post significantly and and fairly frequently on clean architecture inet soet seems to have really embraced it uh and
I don't know what the heck people are doing in in in the Java World um you'll see one conference talk you know one talk
per conference in in Java or spring talk about sort of clean architecture even though it's not really clean the way
they're describing it um it's usually some some combination of things uh but it's really it's really interesting like it
doesn't seem to have the Mind share in the Java community so it's like I don't know what the heck architectures designs
people are doing maybe it's all had Hawk and this is why people are having problems I don't know all right oh we got our
prediction wrong we did but um Jonas got got it right Jonas got it right well 5050 we we'll give we'll give Jonas we'll
give Jonas half a point because it's it was 43 or 401 like that's better than what we did um so zero yeah so this one is
uh because We we forgot our good old CSR didn't we turn did we turn csrf off I thought we csrf oh it is a crsf right
because we don't import this config in our tests yes ah let's let's just add the token um I think that's the easiest way
to or we could disable it for this test what did we do elsewhere I know we did this before so let's go look at our that'
s that's that one uh what did we do here do we have a post we must have had a post yeah there it is so we did with cs
thing is that right uh yes you just need a DOT before the before the width pass yeah I don't know if woohoo but Spring
Security maybe woohoo said ironically now it should be the 404 right yes Jon got it right that's a you yeah I don't know
the the this has been happening for a while Simon I feel like uh with all the shiny technology front-end Frameworks
things like that um design and architecture I feel like got pushed to the to the Wayside a bit um it yeah could just be
that that's you know old man yells a cloud I'm not sure get off my lawn I don't know uh uh but um I I feel like people
interpreted certain recommendations the wrong way like don't do big design UPF front turned into um and there is a lot
of fashion uh stuff going on I feel like at least uh the popularity at least in my my sphere my bubble uh of HDMX is
sort of reinforcing like hey maybe hyper media was a good idea and we shouldn't do all this you know front end crap with
all these complicated over complicated over um unfortunately the the the hip crowd uh they they make more money if you'
re with if you if you you know publish stuff and and sell stuff that's uh the latest Hipp is technology you get much
more attention than like hey let me just teach you solid not so ID but like fundamental principles uh yeah fashion
driven development definitely I love the the image on this one yeah and that has not changed in since the when that was
published 2013 11 years ago it hasn't changed and like fashion is is great but it doesn't last very long and you have to
constantly hop on the latest bandwagon and no not for me yeah there definitely is a lot of resume driven de development
I I feel that's kind of hilarious laser just went back to server render by default it's like just render it on the
server it's celebrate should have a uh we should have a um a prediction uh game was like how you know who who has the
the most correct predictions for for for our tests all right um so we get we got the we now fails as expected right so
it now fails with a 404 uh and now let's do the minimal minimal amount of work to get it to pass lower case o I know you
could have done pm I know I was starting to and then whatever mid Midway through changed your yeah this trying to void
right yeah well okay uh this is this post is not a is is should this be a post I guess is the this really shouldn't be a
post this should actually be a get because it's a query um why did why is that example doing a post did I just misread
it and it actually should be yeah it is doing a post no that's that's that's kind of hilarious because like um the one
of the fundamental aspects of rest is uh using the verbs correctly and post you can do for search if like it's a
complicated search and might have some amount of time to to to actually run um or if the search is complex enough that
you actually do need to put it up body but this should be a get this should be a query because it's basically fine just
I'm querying stuff um so yeah so let's let's change our test before we do anything let's change the test yeah Jonas has
has 1.5 points we should we should have a a a leader Poll for for viewers who who predict correctly that's what I
intended because like maybe I'll figure something out yet another yet had another side project that'll I'll have to
create a little app that tracks that all right so we do want to perform a get um we don't need with the with CRS csrf
because we're not doing a post um but you lost a close PR right just to you know keep me on my T that's how I roll yeah
oh second no no no uh shift J yes yeah um now run it again should get a 404 yes excellent yep so now uh we certainly
don't want to return void just said it's a get mapping and it's going to return stuff so the return an array of strings
or a list of strings HTML because what what's going to happen is it's going to take whatever's returned from this and
basically stuff it into the Dom stuff it into the p string um now this is going to be a bit confusing uh because we're
in a we're in a regular web controller um so we're gonna have to do some stuff but not not until we have a test that
drives it um so yeah so let's maybe we want to call it something other than just themes and we don't need the model just
yet in fact I don't think we model themes what do you think that yeah what do you think so this is the list of themes
that the autocomplete will be using now this is Dynam though that's what's interesting about this is it's it's querying
over and over again yes is that GNA be is that gonna feel slow no okay I mean it'll it'll be what it'll be whatever
latency the connection between your browser and the remote system um so if we certainly when it's deployed in production
um there might be a a a 200 millisecond delay if somebody's reasonably far away um but that still is within the Realms
of of what you want in terms of response time got it okay uh so Jonah suggested the name query themes which is what
initially popped into my head um but I kind of like autocomplete themes but what do you think oh query in the sense of
which yeah I think I prefer autocomplete because it's more domain specific yeah it feels like it tells you like what it'
s what it what it's for um the input is is theme query although that that may be subject to change but I think that I
method um yeah don't don't temp Simon I might see yeah with the chat Integrations interesting uh so we got to return
something because we're not checking the content we're just checking that that it's okay it's a bit of a trick question
yeah so fail right this is gonna fail because we're what right now the way this is configured is the return value here
is not content but the name of a view and so there's no view name that's an empty string in fact you can probably see
faintly intellig having the little gray UND wavy underline oh yeah yeah right here uh because it basically says cannot
resolve view with an empty name um that's fine let's run it make sure it fails in that way and then we'll fix it and
then I'll I'll get to your question in a bit so as expected it's like I can't find a template with an empty name right
yeah because it's expecting it to be a template now we don't actually want it to be the name of the template we want to
be able to directly return HTML so what we have to say uh is is another annotation on this method which is exactly what
is being know um so what response body does is it says oh take the response the string we return and that's the body of
the message that we return so don't treat it as a view name treat the return value as unless you've downloaded the
documentation it won't tell you much more yeah I didn't get in that Cho uh we can we can do that later um so now it
should pass because now it it will say okay you want to return an empty string pinpoint uh but we also started we also
we did I don't think we committed before we added the the HDMX stuff oh right so all that is new as well is that even
working um we don't we don't know actually yeah we won't know until we actually write something better okay all right um
so let me address uh D's question which is a common one and I I need to publish a a video on this because it's it it
comes up oh come up every stream but it comes up almost it feels like almost every stream uh certainly at least once a
week um because it's a really good question which is where do you do validation um and there are two kind and it's the
way I think about is there's two kinds of validation there's uh domain specific validation in the in your objects um and
then there so so and this is where the layering that I use which is uh DD plus hex which is hexagonal but where I have a
domain layer those kinds of things you test and and Implement and uh validate in your domain layer um but as as as
suggested sometimes you need to check the database that's in the application layer so the application layer as part of
it doing its job for saying for example register user and you want to make sure that that email address isn't already
there that's the application Level code so first thing it would do is go and check the database is this email address in
use if it is immediately return with a with a result saying hey this email address is already registered um if it if it'
s fine then you can continue with whatever the the domain needs needs to happen um so yeah so there's some validation
that's going to have to happen and whether you call it service layer application layer um I prefer actually alistair's
ter terminology which is use case layer um although he calls it application because the whole thing is application but
the use case layer is the one that has access to IO and this again is why I like the separation between the domain layer
and the application layer the service layer because in the domain layer you can't access the database it doesn't exist
in in your world um so therefore the only validations you can do is this object valid is this request to change State
valid um then there's the additional part which is um don't forget about the validation that happens in the adapter here
this is domain free and what I mean by domain free is is you're doing things that is this thing empty is this thing not
null um is this actually a number uh those kinds of validations H happen at that Lev level um and you will end up with
some duplication of validation across these across these layers because uh your application layer cannot trust that the
adapter did the right thing and it's not that I don't trust you to to be a professional and do the right thing it's we
as humans make mistakes and so a lot of this is about the protection of prevent preventing mistakes mistakes happen oops
I forgot to check to make sure that that this thing was a number and I just passed it through and it turns out it's not
a number your application layer better check that as well yeah it took me years to many years to to figure out figure
this out and and with sort of relating it to the different parts of the DD plus XX architecture um really helped like
just by saying domain it doesn't know about the outside world so it can't do any validation of like does this email
address already exist so therefore that happens in this layer um and it makes it then very easy to figure out where
those validations go um and yes using the term boundary versus versus business is basically idea all right um our test
pass and we committed uh I think the next step is let's return something hardcoded on line 28 and and see if that gets
inserted into our HTML so let's um let's put it in uh let's just return some some paragraphs so we're going to write
some theme that's not far off but we can just use a single word as a as a theme and then let's close that tag and and
sure why not cats and dogs living together um that should be fine uh so let's run so domain services are are interesting
um domain services to me are are used when it you're sort of doing cross object validation um so the you shouldn't be
calling from a value object into a domain service um I would not well I mean I would not do that um to me if it's a
domain service it should be doing the validation before it creates the value object so it sort of depends on on sort of
what might be or not be valid um value objects are generally going to be small and should self- validate uh but they
should not have dependencies I kind of think of if you think of it as sort of you know these nested um layers value
objects are are sort of the innermost things that don't depend outward they don't depend on uh any kind of service um
entities the same way entities should not depend on services so if you look at uh and I think clean architecture draws
it this way is that domain domain services are outside of entities value objects um at least that's the way I mentally
think about it so if you want validation if a domain service needs to validate because it needs to validate let's say
start date and end date and they can't be reversed and they can't be the same right because you're going on on you know
you're scheduling an an event well okay maybe they can be the same day but can't be the same start and end time then you
need to then you're talking about cross Val cross object validation and that would either go in an entity or or or in
necessary all right let's start typing wow um that was not entirely unexpected um log back in uh no uh we need to add
that endpoint to right that kind of situation is what makes uh things a little bit more difficult um so we need to add
it there all okay restart uh yeah that you're gonna have to restart now I saved do that click what you said before I I
saved you not yet joke okay so let's go back let's restart uh that's interesting um back we clearly were getting
something uh so let's how did you see that well because before we were getting a security thing so clearly the it was
being invoked um let's uh let's make this a bit wider so we can open the body and the form and so oh because we put it
as HX post we changed the get but we didn't change G picky yeah uh so you don't have to restart if you do um uh if you
put the recompile and that should and then refresh the page that should do it Go page did you mean that's weird did you
mean to click on that you wanted to click on the refresh button oh shoot yeah I meant it back here okay so go and it's
always going to return the same result because we hardcoded it but at least now we know this is this is what it looks
like got it I was gonna um show what the end game is I wonder if that would help with knowing where we're heading this
was like actually I should have shown what was it yeah so here it's like the names of movies so I could type you know g
d starts reducing right you know and then when you pick one you pick it and then you could do another one you know like
right so that's kind of that right and the and the technical term for for these apparently is uh a pill because it's
shaped like a pill oh interesting yeah so this is sort of the end game we're shooting for right context uh so Jonas
mentions an example of validation of uh an IP that verifies at least looks like an IP address and that's fine you can
examine it and say does this look like an IP is this an ip4 an ip6 um they have a very specific format um doesn't tell
you though if it's sort of valid for whatever usage it's valid for uh but the the Constructor uh or the static method
depending on how you how you do it um would verify that at least it looks like it could be correct it's in the correct
format so you could do the same thing for for email pretty much all you want to validate is is there an at sign and
somewhere after the at sign is there a DOT that's it don't try to write X's please stop don't do that um I'm amazed that
and frustrated by sites that still do that because some of them don't recognize the Plus on the left side which is
totally valid um so don't do that uh then what you want to do is actually send an email to that address and verify that
it works except even there got to be careful um denial of service uh so there's some spammers who basically do these
kinds of things assuming that the site will send out an email saying please verify your email um but nobody checks that
it's actually you and so they're very it's it's like a that yeah you you you try that and see how how well that works
for you first you got to make sure that chat GPT is up and then if you if you trust it yeah all right uh so what's our
next to did we make that service yeah we did right where well we talk to the repository and say give us the themes yeah
so we we could go we don't have a thing that does the subset do we it's just giving us all the themes that's true um it
could hold on to all the themes in the server and not the database every time instead just we could or we could have uh
a version of the query um basically do do starts with so we could either do it in memory or we could we could do it a
lot we like so I generally think about stuff like caching and so on once once we get stuff working um but I think we've
got uh a little ways to go early yeah before that and do we want to start with start with start with starts with or
contained I think they're both just as easy and presumably you want starts with yeah have to think about that because
that example I just showed you again it's not a it's not a where to go here it contains right because it's it's titles
that have multiple words right um themes generally have one maybe two or three words but I would think they're all
phrases you're not prob to like start with why and then it come up with New Year's that that feels wrong for me yeah
yeah starts with so I think starts with is what we want I mean like I said if it's turns out to be a problem later on we
can that's easy to change yeah yeah um let's look at our our jira uh we'll probably want to also do a commit since so we
might want to break this down a bit more from the UI standpoint um so we have uh start typing and and uh returns text or
returns working uh well just uh returns HTML of of all things well right now it's basically just hardcoded so I think
it's just returns HTML that gets put in the right place yeah yes J Jura text is the best Jura yeah um so we got that
done and next thing we want is is I think a a question of how much more do we want to put on the UI I think you know we
could do some more on the back end but uh I think it's the UI that's the more difficult aspect or or more unknown let's
put it that way so what do you what do you think we wondering do we see how that tool or that whatever it's called um
the HTML component that we're looking at what it its needs are and so that we move in that direction or we're not just
we're not well we can't use that component because that's a react component oh at all we can't use it yeah we can't use
any any predefined component because none of them are going to do what we want to do oh I thought we had we found one
that would work for us no what what what we're doing is using those as as telling us how to implement the HTML side of
things got it but we're gonna um because they all assume that you're you've you've pre-loaded all of the choices um not
to mention that the react one is react and we can't use anyway right right oh for some reason I thought one of them was
an htx based one or something like that I didn't look at him closely I oh okay yeah no a usability standpoint right
right and so we're gonna we're gonna be implementing this mostly from scratch okay that I didn't know cool learning
something new every day right um so then uh that's why like this this part is the least known because um um we got to
figure out how how how we want the Bas a little bit little c a little bit of CSS and a little bit of HTML and right so
we can go down the road of get the back end producing the right data so being able to search do partial searches with a
starts with um or we can say that's easy to figure out the next step is um okay we got some HTML coming back but how do
we make it so that we can those right because right now it's just right so we want component could we use we kind of
want uh we I think we so what we could do is is sort of uh to start with right below the input field we could have a
drop- down and the contents so then there wouldn't be a paragraph be I forget what a drop down needs I can um oh
basically needs options so we already kind of we already do that actually right below right we already have exactly uh
in the HTML that you've already got open oh oh this one here it is okay yeah we just need we just need options for for
each one so then does that mean it would be an array of strings no remember it's just HTML so it's one HTML blob so in
that string is going to be multiple uh options and so we're going to generate that HTML on the back end and then just
dump it over to the front end I see so this themes plural is a bunch of paragraphs is that what you're saying uh no it's
so we're we're going to do is we're going to generate HTML in the back end that is option name equals this value equals
this right so we're going to generate a bunch of option HTML elements on the back end got it right so it's not GNA be
using the th part yeah because we're not using time Leaf right right and that's a and that's a choice we could use a
timely fragment that would do this for us um uh we could try that that's not the that's not the way I've been doing my
stuff but it doesn't mean that it's wrong it just means that um I have I have different different needs for some of my
stuff um I find it a bit easier to to test um but for this kind of stuff it's not that much more difficult but up to you
which which way you want to go I think going with the I guess the option was do we generate the HTML ourselves or do we
use time Leaf to generate it for us what is the advantage doing time Leaf other than a dependency or the disadvantage it
means we don't have to generate the HTML we just right create an HTML file that just has the option in it uh with the
four with the four each with the with the th each um and let it generate it by putting it in the model um or we generate
it ourselves using basically string concatenation feels like a CO TOS to me like a coin toss I don't have this oh okay
um then let's let's generate the okay hey fnu yeah you're you're a little late it's okay better late than never as they
always say yeah and the reason why I like to generate the HTML myself um it makes it a bit more testable uh but also I'm
sort of heading towards I want to create a bit more of a component like a UI component like uh design where the front
end HTML plus some of the behavior is is connected in some way I still haven't quite figured out how to do that I've
looked at um uh uh Thomas shu's uh view component stuff but it doesn't quite fit the model that I have in my head so I'm
still sort of trying to trying to figure that out um still doesn't answer the question though do we want to do focus on
the UI uh is that what we said well you said the UI was a little bit more unknown so I was I was going for the what go
the unknown okay it's harder and prioritize the unknown over the known so the next step would be to um show the choices
in did you say like list yeah because we may not end up using the uh theop the will well I'm I'm not 100% sure uh so we
might or might not use it depending on on styling and and so on gotcha I want to go back to where did that guy go I
guess I must have closed it yeah so I believe the the the one you were showing um this one I don't know if that's
actually a drop down I'd have to you'd have to yeah yeah or it could just be a div div so it's got an input that's the
input field like we have with right you know autocomplete off and and so on uh and then it's got the div um with a
button no I think it has to uh that's the button for that that you see on the all the way on the right that right now is
hidden um so I think what is uh oh yeah collapse the left side can we do that I don't know let's try it uh NOP what
about this one um let's actually just let's just make that smaller so we want to do is we want to look at when it's
dropped down what this thing do let's do somewhere in here it's not in there it's behaving it's hard to see because it
keeps going do I do control shift C while you're hovering over that yeah can you try that see if that works no it
basically changes focus and so it's yeah this stuff is so hard to inspect is it's weird it's like it's outside the body
is it outside the body that's crazy um it's hard because this is because this is a a code sandbox thing there's
basically a an uh no there we go ah so it's down here this is the the popper um so looks like there's a div here yeah of
course it disappears course it goes away when you yeah um so it's it's this guy uh but yeah I can't can't figure out so
but it looks like it's a div and it's not a drop down is is is what I suspected anyway um we'll have to uh this is
something I I'll do offline is is is look at this one and there's another implementation that I want to look at um but
pretty much and it's unsurprising because what you want is you want a little bit more control over the the design and
layout and so what this does is you click the button or you start uh and it's unfortunate that it loses Focus but I
guess we could implement it instead of being in a sandbox and then inspect it yeah but basically the the the the the
main the main thing that that um we care about is that it it's what we'll want is something like a div uh that displays
all the choices uh and then when you um what's inside the div yeah I'll H I'll have to offline figure figure that out um
because I I actually did take a quick look at the implementation of this component itself it's actually not hard to read
um if if you if you know anything about if you know a little bit about typescript it's it's not terribly difficult um so
yeah so well we'll we'll figure that out offline yeah yeah so we could just go into the the component and look at it but
basically um what we what I think we want is want I think we can we can start with a then migrate to to the other
mechanism although since we're pretty much at the end of today's stream maybe we just leave that as is uh and the next
step then is basically figure out the the different pieces that we need right and then we would filter well they'll come
a point where we need to filter yeah and so once we once we need to actually filter um that part will will be relatively
straightforward because that that's just back end and we can decide do we do the do we let the database to use we let
the database do the narrowing down or do we cache it in memory and and filter it down in memory like how I put some
empty stories there homework yeah sounds good comman so what are we selling what are we we celebrating the end of the
stream or that you're Mantra I wish uh I wish streamyard supported overlay videos but I have not been able to figure out
how to do that I can add an overlay but I can't add an overlay as a video oh that we're still here well we're not here
for any long for much longer I'm glad glad you drop by again do yeah I'm just trying to think there's really yeah so
what's left is is um figure out so we're going to figure out the HTML CSS for the for the dropdown which will then drive
what HTML we're going to return from that endpoint um and we'll also have to figure out for the multiple theme uh do we
handle multiple did we handle multiple themes in the search before I forget what we did can we can we look at that um
when you say look at that meaning looking at the uh well let's I mean we can look at the implementation of the the
Searcher you mean this no no I the I want to look at the so search by theme in the song service is that a single theme
looks like it if you look at our draa we did talk about single selection right I'm just I was just thinking uh so even
when we have multiple themes on the front end we don't have support for finding by way I mean we'd have to look at we'd
probably want to look at our tests um uh that's too high high level we want service so song Service uppercase do we not
have tests against the song wondering oh you were looking at files that's why it didn't oh I was in files not class yeah
so we got the song want uh some multiple songs so let's look at the list of methods so added songs are saved add song
bulk ad song malform multiple songs added or found uh them singular yeah so we don't support multiple themes did we
Define what that behavior is I know we talked about it before but I don't remember what we defined I would suggest
looking for something a bit more yeah I know I'm trying to think hits so we got multiple songs that match a add a song
multiple things right multiple songs we not we did not specify it yeah so what do we want to H so so this goes back to
sort of what do we want the search to do if you add mult if you search for multiple themes does it show only the songs
that have all of the themes you asked for oh I see I would think both both meaning songs that match either theme okay so
basically so so it's an implied or yes okay right because then that's where ranking comes in it's like if you enter
three themes do you rank songs that match two higher than those that or is it uh who cares as long as it matches we
don't care yeah it's interesting one um by Jonas have a great rest of your day yeah have a good one yeah it's
interesting like would useful you way I won't really know till we get some data in there we do some test searches just
to see yeah what is it like well let's let's um uh let's put that down because we can't obviously process multiple
select um unless way of of searching for I don't like the wording of that um uh I was going to say um uh searching for
songs with so searching ah uh can you hit escape to turn off the search uh searching for songs with or yeah I think it'd
be hard to experiment with the um spreadsheet because it's it's strictly one one per column column so it'd be kind of
weird there's no way to there's no way to say find me uh on you know any of these themes just across multiple columns
it's just no I agree I think uh that's a good way to start and whether we want ranking is the open question uh so maybe
indented from that is um so underneath and indented is yeah figure out you um of songs meaning are songs themes I don't
know why I put quotes on uh I would say our songs matching having or something like are songs matching two right and
this is the sort of the benefit of doing ranking is you don't have to then explicitly say I want I want an and or an or
it's or I mean this is why search engines do what they do they're generally ranking and that's um generally more useful
than than than sort of a strict and and where where it gets interesting although I don't know that we have enough data
to to do that is you can start looking for semantic links like find me more songs like this right which it could do
because it it could use the themes that that one has as then an entry of a search so you that like find it is certainly
increasing the scope of the project well yeah certainly a nice to have yeah we've got a lot of other stuff to work on
before that or not maybe that's a user feature that you want to add ahead of contributor features right yeah who knows
all right I think that that does it for today then sounds um so schedule for uh the rest of the week um tomorrow I'll be
streaming solo and that's all I know I'll be on the radio yeah Mike will be on the radio if you want to listen um so
tomorrow I'll be streaming uh Thursday I don't know I might stream Friday I don't know I might stream and that's that's
the week uh and as always um if you want to stay as up toate as possible um Jo in the Discord uh because I announce week
schedule sometimes on Sunday nights sometimes on Mondays um but I do try to do it in advance uh and um uh and of course
there's lots of channels to to talk about the stuff that we do on Stream So join the Discord um yeah it actually didn't
like the word creep uh it auto modded that word sometimes it's interesting the words that that twitch decides to automod
which I totally get but scope creep is is a is is a fine term all right uh anything else you want to say Mike no I'm
good all right that was fun yeah that was good so um so at some point next week I'm I'm sure uh we'll continue picking
it up from there um I'll have I'll have done a bit of homework to figure out at least the next steps for the CSS and
HTML uh to have a nice a nice autocomplete drop down uh until then uh I'll see you on my solo stream tomorrow and have a
great rest of the day take care
