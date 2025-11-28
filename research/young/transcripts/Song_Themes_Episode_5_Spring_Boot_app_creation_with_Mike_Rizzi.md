# ＂Song Themes＂ Episode 5： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=2ESC6MEw3ic

---

## Transcript

all right hello folks and welcome to episode number five of working on uh the song themes app good morning good
afternoon welcome and uh so today uh I don't think we know what we're doing um so yesterday we uh we got to a good place
we did some some good refactoring um we did some uh actually quite a bit of refactoring quite a bit of prepare factoring
we tried out some different implementations for searching uh for for songs by their theme um and I think today uh why
don't we put up the list and see what what's up there okay so yeah so we did all that stuff um can we check off number
seven s yeah I think we can welcome um so yeah so we can we can find multiple songs that match a single theme um and
there and I can track songs that have different themes so we were refining our language a bit uh and I think the only
unchecked checkbox uh the only open jira we have is is 21 um so maybe we should work on that should we work on that or
do you think we should think about what else we need to do next and then decide if that's next um I'm actually not sure
what else we could work on next that I I think we should I think we I mean I think I I I like to have full full top to
bottom outside in complete before I start thinking about other features like for example searching on multiple themes at
Orem stff checkbox wouldn't be sufficient then sorry I didn't mean to cut you off there um it's a start yeah it's not
it's certainly not enough right right should we add one more at least um or you want to go and do it first let's go and
do it I have a feeling it's going to be mostly HTML template work uh for um because we have we've put in the model uh
the single song basically any songs that match um as well as no results and so it' be nice to actually HTML hey there m
uh L Sai or C welcome and astd nice to see you good evening so so this yeah so um I I have to say I am I am very r Rusty
uh not Rusty uh I I don't know how or if we want to write tests for this um that because I'm a bit I'm I'm honestly a
bit Rusty on on on that so uh we can we can figure it out or uh we can wait for some of that testing and preparation
yeah I was wondering about that too about testing ah Muhammad no worries yeah usernames are are always uh uh interesting
let's put it that way I'm glad you made it out of dependency hell astd that's not a fun place to be I've been there so
sorry been there done yeah um what do what do you think should we should we just I mean certainly the the first one with
no results uh we can so one of the things I I I think about when when I'm when when sort of think about the UI and
testing is like how easy is it to sort of manually test and how sure am I that uh or how confident am I that stuff
generally won't break and so one of the things I found um when doing ensembl is I had had um logic in the template so
you can put logic and templates you can have sort of if statements and switch blocks and that's terrible um and I don't
know what I was thinking uh but um it meant that that I ended up having having quite a bit of what's essentially code in
my template and that's just bad because I didn't have any good ways to test it um kind remember the I think fer had the
what was it called the presentation model approach where you separate out the any UI logic yes into a testable ENT yes
yeah thing I don't want to say entity because I don't mean database um and the UI is just blindly just doing stuff based
on that yeah and so one of the big refactorings that I did for ensembl recently when I was adding The Spectator feature
was um pushing all of the decision making about what to show what not to show what buttons were whether buttons were
disabled or not what the text of the buttons were all of that was pushed into actual real code as opposed to uh pseudo
not pseudo code but like not not quite I mean it's code but it it shouldn't be you shouldn't have code in templates um
the templates should just be mapping right they should just be and doing very little mapping at that like they should be
almost exclusively about presentation um and if they are almost exclusively about presentation uh and because we're
going to be using time Leaf which means we can preview the template uh in a useful way um I generally don't think much
about testing that stuff yeah so um at least a start I think we can we can avoid that and we can uh revisit that
decision later on sounds good hope you don't mind me typing um no that's great I like to sort of blurt it out I'm
actually hoping maybe it's too cool um well I have even so pH ask can you use end to end testing tools we could um
probably what I would use in this case is is HTML unit uh because that's exactly what it's for um but uh again we're we'
re going to now translator interpreter Excuse me yes I can't believe I got that wrong let's see since my partner is an
interpreter and I know the difference between interpreting and translation um so I was starting to say I know well you
were saying you know HTML testing not your Bailey Wick um time Leaf is not my bailey Wick so this is going to be an
interesting Adventure um looking forward to it so yeah for for this stuff it it'll be relatively straightforward because
um because we're not going to be using much other than time leaps insert text from model here and and you know if if you
put aside all all the other stuff it's pretty much just replace this text with text that's coming from the model got it
otherwise it's an HTML file the other thing that might be something that could be interesting that we do today is we
haven't pushed a production yet and I know we talk about this right two sessions back um and we talked a little bit
offline but I'm thinking at first I'd like to do push to production but have a feature flag where users can't see it
people that navigate to that site don't see the UI but maybe we could have some sort of of feature flag where we can see
it um doesn't have to be sophisticated like you know from coming from a certain IP address but it could just be Noah
magic incantation right like I don't know so secur security through obscurity yeah exactly security through obscurity
like that um I mean the problem with that is if we do that on stream then it's no longer obscure yeah but really that's
fine I mean you could just put you know we could just put a uh we could put it at an endpoint that is not linkable from
the homepage which is actually what we have now right it's not linkable the homepage is completely divorced from
everything else uh and the control the controller that does the search has you have to know the link so already it's
it's security through obscurity yeah I'm gonna call that phrase of the day security uh full says sometimes it's simple
to put logic in the UI and we've seen that in many projects uh what's the argument to not use logic in the UI um the
logic to not use you logic in the UI and by Logic we mean you testing an expression um an if statement switch block
something like that if you're doing that in the UI you now have logic that you need to test so the downside is you now
have to test that uh manually or hopefully in an automated fashion um oh sorry and the disadvantage of an automated
fashion is those high level UI tests are the most brittle of all the tests you can write and so yeah and so then you
need to design your UI um depending on what you're doing in your UI um is you want to to then at least separate the
logic from the actual presentation even if you're doing it on the front end uh so if you're doing react or view or one
of the Frameworks you want to make sure that you've properly separated the logic part the decision-making from the
presentation and so that way you don't have to test through the brittle actual UI that is bad you don't want to drive
the browser except for maybe some sanity tests but you don't want to do a lot with that um the advantage at least for
spring boot with time Leaf uh or any serers side generated code is if the server um generates all the information then
the front end is only presentation and that's what we're going to do we're going to basically just have um there may be
some cases where you have to do a you still have to do a little bit of logic so for example we're probably going to have
to do uh a tiny piece of logic which is if there are no results we'll show this if there are results we show the results
so I don't think there's any way you can get away from that other than having two completely different pages um one
which is which is showing no results and the other which is showing results and you could do that and then you have no
logic then the logic is is 100% on the back end deciding which page to present um and now that I say that I think I
actually like that better um because then you're really the page does what it does it says I'm supposed to show no
results I will show the page with no results who decides that that page gets shown that's the back end um so if it's all
in the back test um I don't think it's necessarily hard so the difficult ulty of this depends on how complex your UI is
um and I think letting really thinking about all the decision making can I let the back end decide this like what I just
said is is is exactly that it's like instead of having the page alternate between two things depending on some
information coming from the back end show completely two different pages I can imagine Ted that if in certain teams
where again not an advisable team structure but if there is a team structure where there's a UI team and a backend team
now you're going to have challenges with convincing the UI team to work in that fashion yeah and I could see you know
they dict things yeah and that's going to be a non-starter and that's that's how Conway's law you end up with the
structure of a front-end complex application at a backend complex and the two don't talk to each other as well as they
could if they're all on one team yeah yeah that's why when when we're doing consulting it's always immediately one of
the first things you say to managers is like you can't have two separate teams for yeah front end and back end they have
to be one team y yep and and this idea of pushing of of going away from complex front ends um I'm hoping is a pendulum
that's swinging back uh that's my hope so HDMX is one way to provide more interactivity on the page without um pulling
in a very complex uh framework and I know people say well react's not a framework it's librar like yes but the way most
people use it it's a framework and the main issue is the complexity and and the immense amount of logic that's often not
well tested on on the front end for some reason I can't post to the comment section I did throw um on in our jira line
25 that link I also to send it to you privately if you want to oh the reason why is because it's my stream um uh you
can't post links through YouTube YouTube suppresses the links oh really yes um which is very annoying uh and that's why
I don't like YouTube's chat posted I don't know why that opens in a weird I'll blame streamyard for that oh the opens in
a new tab that's interesting it it appended that with no space I'll post that again yeah so that's the presentation
model pattern uh that we were mentioning it's really interesting how how uh I know I take for granted a lot of stuff in
that book uh patterns of Enterprise application architecture some of it I think is is now considered sort of obsolete or
not current practice um but there's so much good stuff in there as as is usual for fowers fell stuff p oeaa is the is is
the title PS of Enterprise application architecture that's where things like repository and and and uh data transfer
object and other other granted all right uh shall we do it should we do it I'm I'm up for it so we're going to work on
jir line jira 21 yes um we probably want to have uh uh if you really want to add another check check another Jura um we
can have one that now gen now that's that shows uh results so life says I feel like the Fowler patterns are more
important to know than the golf patterns I think that's probably true for for most people um especially since of the 23
go golf patterns I don't know that I use more than than five or six adapter strategy maybe decorator all right uh so
let's work on Jura 21 I guess if you implementing undo You' use command but not many people are actually implementing
undo that frequently well command does come in handy uh with event sourcing oh that's true yeah yes luckily we we are
allowed to to to read whatever we want um unfortunately nobody does read g a four book or poeaa in their original forms
they read reinterpretations and misinterpretations so I would love it if all right do we have a template at all what
have we got in our in our uh resources templates so we do okay and what does it look like it looks empty awesome um so
what we're going to need to do is uh turn it into a Time Leaf template so let's do that I will more uh direct
instructions yes I am going to give you go from high level intention to yeah uh so the first thing um uh to the to the
HTML tag on line two stick a new line before the closing uh bracket and then uh now in two and a half what we're going
to do is we're going to add xmlns and then colon and then th and so what this does is it tells the browser and other
things that are interpreting the document that anything started with a th is in this name space um it's technically not
required I think uh but it's always a good idea to have it um and so we're going to assign it the value so it's going to
be equals and then in double quotes uh it's going to be HTTP colon SL slash uh www.tim lef.org that's it you know this
is a tangent tell me if you if I should just not do the tangent we're here for I often so so some side still default to
www. you know domain. um Com or whatever right and others don't is there any particular re I mean for me it www. just
seems so 1992 um and I just like why do folks still do that for their websites is there some technical reason yes there
is a technical reason um uh so DNS uh which is which is a fascinating area because it underpins our entire internet um
and if you run into a problem usually it's the DNS is the old saying um but um also tangent on that tangent I always
thought it was the I remember when there when there was sort of the possibility that web dot instead of www could be the
could be the prefix and I thought it was the stupidest thing to to take the letters in the English language that are the
most number of syllables doubleu doubleu right three three syllables for each letter so now you have nine syllables to
pronounce it as opposed to web which is one syllable but they chose www um well that was that was that was what came and
so the technical reason is that uh the domain name so Tim lef.org for example uh you have to do some some special stuff
that not not all DNS servers and not all DNS setups support in order to uh basically rent give you the IP address of
where you're going to go and and fetch your your and basically send your HTTP requests um so there are probably some
servers out there uh where you can't set that up or your DNS registr can't whoever is providing your DNS doesn't have
the ability to set that up um these days most modern places where you're getting any kind of Hosting will make that
relatively straightforward uh and sort of do that behind the scenes but it is it is a bit tricky uh because you have to
do some C name and there's like there are articles written about this particular thing so it's not just random um but
luckily it's it's relatively straightforward in in the modern internet and people who are doing it either don't know or
how to do it or it's not supported uh but easily supported by their their DNS provider yeah I I know that website I got
for redirect right where it's like if you type in www. time.org just and that's pretty that's pretty common because you
still want to support that um but if you don't but you don't want people to to bookmarket or land there shave we're all
we're all about the tangents and and such here uh p is book was published in 2002 which means it's 20- year old um if
you're going to read one book either POA or refactoring read refactoring absolutely 100% if if you can only read one
read the refactoring book um the the the Enterprise application architecture patterns book there's G I think it's still
useful to read though there you're going to have to keep in mind that there is some stuff that's no longer common uh
good current practice um but I I certainly think it's it's still valuable to read and and that leads me to a little bit
of a of a rant which is just because a book is 20 years old in computers does not mean it's obsolete yes if it's a book
on Spring uh 20-y old book is not going to help you but if it's a book on more fundamental and especially patterns it's
likely that it's going to be a lot more relevant um some of it will fade right like I don't know anybody who really uses
the bridge pattern much anymore except in very uh specific cases of probably writing some Frameworks um but we use
strategy we use adapter we use Factory methods we use we and there are more than just the 23 gang of four patterns right
there's hundreds of other patterns uh that are that are also useful and this book of patterns is is an additional set of
patterns so patterns are are generally longer lived and still useful um it doesn't Ma and the original refactoring book
is 25 years old and it's still super valuable almost everything in in that book applies other than the data Java syntax
but the refactoring still apply yeah now what's interesting is I haven't actually read the new version of the
refactoring book where they where fer changed it all to JavaScript right um I'm sure there's some learnings in there
about you know since the first version of the book yeah which book would you recommend folks read the Java one or the
Java one is 25 years old or the JavaScript one um years old I would probably read the Nar so both I'd probably read The
Narrative of the newer one because I think the narrative is much better um but uh I personally don't like that he
changed some of the names of the patterns to to sort of more match um JavaScript so you know it's it's some of the names
renames are are fine but a lot of them are like from method to function I'm like to me everything's a method like I know
JavaScript it's called functions but I I like the word method because I'm in Java so um but either is fine I mean it's
probably difficult for most people to to get a hold of the 25y old one uh I happen to have several copies but um if
you're on O'Reilly's learning platform do you have access to both and to me I think that's I wish I got a commission but
I think it's well worth the cost if you're doing any kind of reading to to get a subscription to that because then you
just get all the books and you can dip in and out and read chapters from from different books without having to buy the
whole book which is is a good way to consum them that's a good if you're working for a company versus working solo it's
highly recommended yeah try to convince your manager director of engineering CTO to get it for the whole company because
it's super valuable yeah and there are companies that I know that that already do that and so if your company does it
make sure you take advantage of it because um lots of good stuff there hey Bel looda welcome all right so we got our
name space uh let's go uh we can keep our title that's fine um and let's see what do we want to show uh why don't we uh
close the project window and let's open up um the controller at the bottom uh so we've got um what are we going to end
up with we're going to end in the model so we've got empty search results uh so let's just create a uh a part of the
page that just shows the value of that of that attribute kind um so after so 10 and a half let's add uh an H2 and um
inside that H2 um in the tag or in the oh yeah in the text uh and so that's going to so what this does is says replace
at runtime when we generate the page replace what's inside the h2 tag which will type something a placeholder um that
gets replaced at runtime with the value of this expression that we're going to write and so the value of this expression
uh so it uses the dollar sign curly brace pattern so dollar sign open and close curly brace and then inside that is
basically the name of the attribute which you have in your clipboard and so here you can yeah you can write placeholder
uh and what's nice so this is one of the advantages that I think as problematic as some aspects of time Leaf are uh that
it still is is for me the de facto view engine for applications is because you can preview this page and it's just HTML
um there are some newer templating uh tools that that move away from this and I don't know why they do that because this
is to me such a valuable thing so if you hover and this is the thing I I dislike in general has hover so if you see the
stuff in the upper right see that those little for four browsers oh yeah they hover so if you click on one of those
don't click on that one um don't click on that one let's click on the leftmost one which is intell so this will
basically open up a browser inside intellig and preview this page so go it uh yes got it got it and so we can see the
preview right we got the H1 and we got the placeholder text and so um this is possible because it's an HTML uh page um
at runtime it will obviously look different because the placeholder text will be replaced um but what this allows you to
do is it allows you to design your page and see what it looks like without having to constantly run it through the
server to see what it looks like which is what H what you have to do with like JSP and velocity and mustache and all the
other template engines because they're not sweet now if we had stuff on this page that was using static resources like
images and so forth would this preview pull them in it would okay y yep yeah I mean basically it's a it's an embedded
browser window um but you could launch it in in Chrome and the same thing would work uh what ends up happening is
intellig ends up running a little web server because intell has everything inside of sorry uh so that looks fine um we
can go ahead and run it and see what happens yeah you can close a application it so shift F10 to run it Oh I thought I
was running it this is a common thing yeah selecting the configuration does not run it right and that's why I don't use
that dropdown um I use the popup because then it will run it when you select it got it and it'll run on Local Host 8080
uh and so we need to make sure we go to the path which I don't remember what it was me too the bottom window scroll up
no search control W there we go it worked that time for some reason it was starting to go outside the uh so be careful
um you have Oh yeah double switches yeah which is technically not allowed clearly and is a security viol can be a
security violation okay uh so we didn't this is not this is not uh unexpected we didn't have the parameter so let's add
the parameter so put a question mark at the end and then add that requested requested theme equals where is it it's not
going to be in there it's going to be up in the request PRM oh and then equals and you can just say something so it's uh
did we actually add in our startup did we actually I think we added a a song but what did we add and that would class
this one s application yeah so let's do a search for for New Year's and we should and false yes absolutely it should
fail gracefully uh we have not added that functionality yeah we don't have a test for that so what I'm going to search
for Y uh quotes nope just leave it it'll it'll URL encode the space for you oh I see you did that hey F hey cool so this
is our manual test and so therefore we have proven that the template is showing the actual results uh so you may have
missed it uh Dill 50 uh we're not writing uh HTML tests so that's why we're testing it manually because uh the template
we just want it to show what is ever in the model and assume that the model is correct because we have tests for the
model and so since this is Java we're basically using jit um but we're not use we're not as I mentioned we're not we're
that uh have we run the test lately no we haven't run them today um but we did run them at the end of yesterday uh we
could run all our tests if you wanted to but thank you for asking about did we tests and it's cheap to run them except
for the yeah except for the M all our tests are passing so sweet um and so since we've manually tested uh I think we can
close J 21 woohoo and now we want to show results for real instead of just uh well actually we might have prematurely
closed it so we we might have had a convers ation with our customer and said I don't want to see true or false good
point so now we have to re our Jura um uh but we could do a commit here and just say we've uh yes uh we could we could
do a commit here yeah because we have minimal uh in a sense we've done our our our it's passed our manual test of
showing the attribute attribute I would say um see I like it what I wrote but uh so we able to see the the results
attribute the search the empty search results attribute yeah that's better using the language of the business domain not
the computer engineered domain cool uh and now now let's let's make the page a little bit nicer so let's go back HTML um
so here's where where we could make it a little bit easier on ourselves by by putting whether the search results are um
I I don't I don't even want to do that I want to I want to have different pages um so let's make this page uh the the no
songs found page the empty search results page so you mean like save sorry keep going so um if we're going to do that
and we're going to return different values for our get mapping um we're going to need to write a test because we're
changing Behavior right so let's go to our controller test uh and then let's look at our uh controller at the bottom and
so what we want to do is we want to write a test for this meth method if there are no results we want to return a
template that has the name so I think we're already checking for um so search results returns models with non-empty
search results uh right so the one test above it tests is the one where the search results are empty so if you bring the
view yeah so bring keep going yeah so search result returns model with empty search result so I think we can update this
to say Nota uh in fact to a certain extent do we even need this in the model at all if we're going to show irrelevant um
but let's let's let's sort of do that as a parallel change so let's additionally assert that theme search uh and so
we're going to have to hold on variable um yeah so we're not pushing to production yet because uh our customer hasn't
figured out uh how we want to do yet we'll do that we'll do that soon yep um like how it CHS Christmas is the yeah it's
pretty uh we want um basically uh this is going to be the what do we call it um template yep uh so let's let's write one
that that passes and then we'll make it fail uh and then uh and then we'll fix the code okay pass it yeah it's un
pattern we're basically just ratcheting up the assert um to match the existing Behavior so we're sort of backfilling an
assertion this just how I talk about it yeah so we'll assert that the template name is equal to uh theme search results
um so that should still pass we tests do you want to learn the popup run oh sure cut I was doing shift F10 on that one
but so shift F10 runs the current configuration but if you want to both select and run um it is uh alt shift F10 alt alt
shift interesting combo so now you can select and if you select and hit enter it will run it so to me I don't use
anything else because why would I um do you always use it even though you've got the current config if the current one
matches I'll probably just hit shift F10 or control R um but pretty F10 that's called The Run config cool all right test
passes great now um now let's make it fail so uh we'll want name um open to suggestions on what to call it we can call
it empty search results we can call it uh no search results theme search with it's basically going to be whatever the
whatever we want and it'll become this file name right is there value in having um as far as using these templates you
know theme search hyphen blah blle being like you know no results from a sorting perspective I I'm not jumping out at me
one way or the other I think theme theme- search- no- results is probably good so we can and we'll we'll we'll basically
just copy that file later but we're not going to do that now because we want a failing test right so yeah there is a way
uh there's um infinit test is a plugin that basically does that uh and there is an intellig added something recently I
don't know if it's quite that I have to go look at it I I haven't explored that yet there is a way to to also do that um
of course what causes your code to be compile does it happen automatically so infinite test what it does is when it sees
changes in the code uh then it then it kicks off kicks off the tests um I'd like to try that plugin again I turned it
off for a while I'm not sure why uh I think it there was something that wasn't quite working right um but we can we can
try that think I need even have it installed idea yeah I think the first time I saw it was maybe 10 years ago where um
what's his name actually it was probably the same conference we were at the one in um San Jose where lellan was um I
can't remember the talk he gave but he basically had it set up that every time he hit control s to save the file it
automatically kick off compile and run every time I was like that's cool yeah I remember seeing it as an eclipse uh
thing that would do that all the time because Eclipse uh you'd have to be more explicit about um sort of saving uh and
every time you saved it would it would build and run the tests and infin test is a plugin that's been around maybe not
under the same owners as it were uh but it's been time whoa yeah so that's the thing uh that's that's the one thank you
astd um it'll automatically rerun I haven't I haven't tried that out I have to see see if it sort of fits my flow so we'
ll check that out out have a compare and contrast session yeah all right so uh we decided on our name so let's go make
our test was this one so this is one of those uh less known about tdd things which is you don't always write a new
failing test sometimes you modify an existing test because you want different behavior and so here we want different
Behavior we want it to be this template name if we run it it should fail because it's not going to return that one let's
go ahead and run it is there um a name for that kind of sort of incrementally ratcheting up um a tddd style test is it
in other words when you're sort of modifying an existing test is there a common name for uh when we say in the tddd
write a failing test um people assume that means new but we didn't we never said new uh but I don't know that I I I'm
pretty sure we're not explicit enough and by we the people who talk about and write about tdd are not explicit enough
about it does not have to be a new test an existing test where you want something different modifi test is a new test
now we're getting philosophical because I'm going to argue you know thesis's ship where it's like it's the same test
even though it's been modified no longer looks like it's original so it's like if I if I have a hammer and I replace the
head and then later I replace the handle is the same Hammer now we're getting to philosophy philosophy uh and absolutely
uh it is it is recommended to do scard tests if they are no longer providing any value um Del leading test and figureing
out which ones to delete is sometimes difficult but definitely uh tests do not forever um okay failing tests test fail
for for the right reason uh let's do this though let's um uh we we don't we know how to fail so we're good uh let's do
the simplest thing that could possibly work so what's the simplest thing that could make that controller the absolute
simplest would break other tests well do we know that we don't know so let's check know so let's Point yeah so let's
just do that I I don't think we're checking for this anywhere else um even if I was though I would do it this way
because i' I actually want another test to fail right because if it doesn't then that means we're missing a test exactly
um or if not a test we are missing an assertion right love it okay firing off the test yes oh good we did test for it
that's awesome is it a different test yes it so search result returns search results view yeah so we did test for it
awesome cool and we haven't written a test for no so oh we did right here that's the one we just modified so that's good
so um and and this is something you know that especially when you have a lot more tests than we have uh I always tend to
do is and this is why I like doing the simplest thing because it would have been very natural to just immediately jump
to if there were no results return this view name otherwise return this template name um we have to might want to make
our names more consistent I use template name but technically it's the view name so um but that idea of let's just
change it and if no nothing else fails then we then we find out that that we are we are missing some assertions um but
Lu we're not uh so let's uh let's rename template 34 yeah Flappy or flaky tests are the worst and I basically either get
them to work or delete them because they're not they're not serving people yes it's like it's twisting their around
again to write it and then it's like no no you can delete this like no darn it I spent a lot of effort to write this I'm
keeping this around even though it's not providing any value anymore doting in general is one of our challenges as
software Engineers loss loss aversion is a cognitive bias um so uh clearly the the simplest thing that could possibly
work did not suffice uh so let's go back to uh so let's go um and since returning a hard-coded value is not going to
work to suffice for both it so you want you want a shortcut to make that easier Control Alt t wait you're missing uh can
you put the semic Clone back yeah yeah so on on the thing that we're going to basically wrap with an if block because
that's what we're going to do right we're going to wrap the return value with an if block um so just put it somewhere on
that line and now if you do T now you can say surround with um and we're going to do an an if else even though
technically we could do a mapping but we'll do an F else and so it basically wrapped it put it in the if block put all
the braces in the right place and lets you start typing so if found songs is empty yep and then else and we think that
this will work at least I think this will work I failed uh I wonder if our test was broken so I noticed this before this
test looked weird um and now we've proven that this test is weird so this test is is was was initial test um and uh we
need to fix it right let me see if I can figure out what's broken with it okay we're getting a new song search with one
song we're asking for a theme search of nothing right that's kind of weird yes so initially we did this to basically
just say if we call this controller method we should get a search theme search results View right um but now that view
is depending on both what the song is in the Searcher so what we're configuring in our setup and what we're asking for
right there in our theme search um and and we don't want applesauce we want which we're gonna have to yes inline this so
we need to inline it yeah it's only get one occurrence inline the whole thing yeah it's only occurrence let's it so the
big cheese asks uh advice book on tdd besides tdd and action by kek so it's actually tdd by example by kek um it's a
fine book uh but it's not enough um so uh growing objectoriented software Guided by test is useful but it does have a
different flavor of testing um but I think it's an it's an excellent book um there are some there is a newer tdd book
that I do recommend uh and I'll I'll dig up the name um I've been skimming through it to see if if it's something I can
recommend um do you want to make what about um I guess it's not tdd I was thinking about the you know the book that's
like a brick um you mean the test patterns the xunit test patterns yeah what is it Gerard Gerard maos uh that not really
about tdd uh it's not about tdd it's about but it is a in my mind it's a prerequisite to tdd because it tells you how to
write good tests yeah um however it is a it is a brick it's a 900 page book uh and it's it's an excellent book um but
nobody's going to read it uh so this is true so live says learning by example is the best way um learning by example and
learning by doing uh especially is the only way we learn um reading and watching can inform you but that's not learning
how to do it you have to do it um and this is where uh testing Kata is basically little applications that that guide you
in down a certain direction now some people love FS buuz um Steve quo is one of those folks who just loves it I hate it
with a passion um and the reason why is it is just too simple um and even if you're learning tdd for the first time I
think it also promotes this idea uh where um it's very sort of technically oriented it ends up being very technical uh
but I would say try it out see how see if you like it um if you don't like it there are other good examples like uh the
expense report c um but honestly it's it's uh it start with just something simple um uh follow some tutorials do it but
you have to do it that is the most important thing is you must actually do it Hands-On keyboard it's best if you do it
if you can with others even if they don't know anything more than you um learning with others learning is social uh and
so that's sorry yeah the Roman numerals one is also a very simple one um that one I think I like a little bit better
there's just something about fizzbuzz I really don't like I don't know I mean fizzbuzz is screamingly non-ob oriented
yeah you can force it yeah and maybe that's why it's it's like because I'm it's there's almost no code where where I
feel like I'm I'm doing code like that so all right um do we want to uh format that line a little bit nicer yes uh you
if you want you could pull song out into a variable otherwise just add some new lines either way well we're going to
need you mean as far as that goes no I was thinking the whole song Oh the whole song right yeah let's do that I can't
even see it though so I want to do this oh I just trust you can trust control W uh I don't even do control w i just
trust the the control oh that inline so Control Alt sh yeah working on it um don't tell me don't tell me V for variable
yeah oh so Control Alt is is almost always going to be your refactoring meta Keys Control Alt V Control Alt P Control
Alt m control alt n control C I was trying to remember the V part was I I was like okay n in line V variable m method
yeah um and I know it and I trust it because I know it's going to select the right expression and if there's multiple
Expressions it will offer those and that's why I don't even need to see the whole line all right I still think it's too
long line so what you just did right the the so undo it and do the the the the join lines you think do join lines versus
just reformat or would reformat no not reformat you want to join lines ah because it's going to do the because it's
going to take away it's going to join them correctly Oh I thought I wrote it down uh control yeah because I see folks
constantly do what you did is like backspace and then now it depending on the indent you might have to delete a whole
bunch of space um and and you can get it wrong and you can get it wrong and when concatenation involved uh uh the
intellig idea will actually do the right thing if we were doing side by side windows I'd think that line was even too
long uh I would agree yeah but since we're top bottom we're okay yeah um so now uh we'd like to fix this we'd like to
search for something that will be found so now I would yeah did I almost put the variable or you know songs um never
mind I almost extracted to another variable and I'm like no no no you want to be able to visually see yeah and you know
to me that's just a preference so if if somebody said hey my preference is I want to pull out theme into a variable um
and use that I would be totally fine with that as long you know the advantage of it as long as that and the advantage of
it it would um you could then do that now it's so now it's named right so you know what the first is yeah and then you
could take the oang sign and basically make that yeah would you do a constant no I'd actually put the text irrelevant
song name because if you turn to a constant then it looks like it's still important mean no I wouldn't that's no that's
not what I meant I meant actually change delete alline sign and say irrelevant song it yeah I like that that's more
clear yeah so the only yeah so the only downside and this is why my preference is the other way is the way intell colors
things so colors strings green um on line 23 three the theme doesn't stand out it's just another variable whereas if
that was a string it would stand out because it's green uh and so I think that's why my preference is to use the
concrete string itself as variable works for me but again it's my preference it's not something I say you you should do
it this way although I don't say you should very much at all or try not to um too much and I need to wean myself from uh
we think this will right yep all right I think we need to update the the method name to make it a little clear that it's
returning uh basically that it found uh songs returns found search um I think we've maybe I think we have and view uh
yes because that's what we're testing we're testing that that's the correct view right so we probably should so do we
want to rename the view itself should it be third theme search found results or theme line number so 25 does that
indicate that it actually sufficient I would think it's sufficient but what are you thinking I was just thinking adding
the word has oh but that's I don't know that that's necessary if it's I I I I was just thinking sort of the the opposite
of of the theme search no results isch has results but yeah I'm I'm cool with that that change can we do actually is
there a uh does F6 work on literals uh not here because it doesn't have the context um if you actually rename the HTML
it might intelly might be smart enough to pick up um that this this file changed oh the file name right right project um
this rename yes but I want you to go back for uh can you open the project no open the project window Okay click on the
gear icon at the top uh and what we want is where always file yeah oh6 so what that does is if you click on the bottom
uh so you can get rid of that so notice that because you're in the song Searcher file it's selected song Searcher in the
project window if you go now to the top it it basically synchronizes them and I have no idea why that's not the default
that should always be yeah I think that should be the default yeah you know what I'm doing one second yep so fful says I
thought it was never mind what about tidy first tidy first is great but it's not a tdd book um tidy first is is useful
uh as is most of kck's writing um but it is not a tdd book so now that it's synced up oh we got another question go
ahead now we're synced up with shift F6 yeses okay sweet and it's got to search for references and search in comments
and strings we just be bold and do refactor or you want to preview oh no I never do preview just refactor it okay so
let's see what actually changed so let's go uh so it changed it uh it changed the controller would be my expectations
let's go into the controller and see what it did you can close that window yeah uh so it did change it because it knows
to look for the controller's return value that returns view name so it did rename that um now the test I doubt it
changed the tests but let's go look at the tests yeah so if we run it now the test should fail um but we can we can just
fix it we don't failure sweet um so are all our tests passing now uh all IO free were I'm G to do all yeah let's do all
because I think it's anything oh interesting oh it's alt I did control I'm not used to alt shift as a now we want to do
all nothing is intuitive this is true it's all learned yep cool oh somebody failed did you expect it uh I suspected um
because we only have one template so we returning the correct view name but we actually don't have the no results
template yeah yeah that you do a save as just to have another one or would you uh you can do y do we want the we want
the contents to be different do we uh I would probably say yes let's go back to the one that uh um or maybe the the no
results and title that work works for me let's see if that test yep we're all good pass sweet all right so Dr nefarious
asks I'm interest interest interested in do encoding via twitch how you do it without inviting people to dox you or to
accidentally see any Secret so I'm not sure what you mean by inviting people to dox you um but uh accidentally seeing
Secrets is a problem so the only recommendation I have is be careful and and have dual monitors uh yes it's you I don't
I I think it's really difficult if diff very difficult to do it with one monitor I used when I started streaming though
I was streaming from my laptop um without an additional Monitor and you can do it uh and so you just have to be very
aware of when you're going to places that might have secrets um in which case you want to make sure you have a button
that that hides your screen um but other than and other than that just you're gonna have to be really careful and you
will reveal API keys and you will then have to rotate them um that is that is a fact of the streamer's life is
eventually you will reveal reveal stuff I suspect um besides my loving the name Dr nefarius as a as a twitch handle um I
think the inviting people to do you is more about um at least the way I'm interpreting it is um yeah okay they just they
just yeah that well if you're not interested in advertising your username on GitHub I'd question why you're streaming
because the whole point of streaming to me is that you're sharing information if you don't want to reveal your GitHub
username um you're going to really limit yourself in terms of what you can do so one thing you can do though is you can
change your GitHub user you can create a new GitHub user account and that's basically a throwaway um and so if you do
have stuff where you want to keep that protected create a new username for your windows username or your Mac username or
whatever create a new login account uh if you want it so uh those who who are better disciplined than me is is you
create new logins for your computer um that are specifically for streaming so you don't have stuff that accidentally
appears on desktop don't have accidentally stuff that appears in various Windows um that you are dedicated that that
account is dedicated to streaming um that is the the best way to do it uh and then you make sure all your logins and all
your passwords and all that kind of stuff are are oriented towards that um and so if you if you do want to be careful uh
that's the way to do it create a new GitHub user account create new user accounts for for everything um because stuff it
like you email address is even is going to show up in the Stream because you won't even notice it um and so having a
separate login will will help with most of that I don't I am not that concerned uh but that's me uh and so if you are
more recommend um this is your alternative is just have nothing of Interest no a value but that's that's a yeah I just
realized we blew past the one hour point should we take a a five uh yeah we can that's a good good opportunity for for a
break because did we commit or did we just about to commit I think we're just about to okay let's bring out the screen
and then we'll we'll take a break okay oh we did a lot without yes whoops mostly renames though true true yeah um so
let's take our break and when we come back we'll we'll do the commit okay we'll do the commit sounds good and uh break
all right and uh just a reminder folks uh a lot of the stuff that uh Mike and I are doing here on stream and that I do
on stream when I'm solo streaming um we discuss and talk about in my Discord so my Discord is a free community oriented
towards Java development tdd data uh domain driven design all that kind of good stuff um and so you can find that uh at
ted. deev Discord and if you want to know about me and how to contact me and find me on various uh social media like
Mastadon or LinkedIn you can go ahead slout all right let's go write that commit comment sounds good oh one thing I was
gonna say um for live coding talked about OBS um we're actually using this which I know you're you're still playing
around with um streamyard really if you're GNA use it you got to pay for it because unless you're happy with 720p
resolution and some other limitations um if you're doing so if you're doing solo streaming I don't think streamyard uh
at least for me doesn't provide what I want from from solo streaming I want a lot I want a lot more control I'm willing
to give up some of that control reluctantly uh to make it easier on on my guests um but uh streamyard is just not as
flexible as I'd like it to be so when you go solo do you um use the obss config yeah so I get more control over overlays
because I wrote that code um and I get more control over the different views uh I can bring in other images and other
things that are difficult or annoying to do uh with with streamyard um yeah so but OBS has a has a Hu it the learning
curve is steep um you can find good tutorials and and it's also uh these days pretty Rock Solid but it it is there's a
lot of terminology and there's a lot of you're pretty much the the outof the Box experience is is it's a steep climb
whereas streamyard is just you go so um if you don't want to spend time fussing with with layouts uh then you can find
something like streamyard and and that'll that'll be just fine but recognize that it's going to limit your resolution
unless you pay for it which for me I did right not sure what to say for this commit um maybe introduced separation of
yeah ship it although technically it's not ship it yeah um so I think we can change this HTML page to to basically say
uh instead of songs it's basically no songs found that be an H1 and then the place and I think we don't need uh the
empty search results H2 anymore um because I don't think we actually need that attribute anymore so I think we can we
can clean up a bit so if we go to our other results page um here we know this page is only going to be shown when we
have line now the tests will all still succeed right they should all still pass pass yeah uh so full n the the tdd book
I mentioned by U by Alan Miller I actually skim through it I actually know him um and it's it's it's good um it's got
some good stuff in it uh but it's it's more than just tdd um so there's a lot more more stuff in there some of you know
two people are rarely going to agree on everything um but in general uh I found it I found it to be to be uh good enough
for me to recommend okay so I put the link in there in the chat all right uh and since we no longer use it in the page
um let's go back to our tests one second yeah I did something wanted to make sure they ran ah okay yeah they did test
and uh let's go to the next test one and I think we can drop this 37 um do we have are we asserting that elsewhere I
thought I don't know if weting elsewhere we'll find out when we get rid of it so uh yeah so let's go into our I think we
were we were looking for it that's fine we can go ahead and and then test yep on line 50 so let's go remove so I wonder
if that if we can combine the first test and this class I mean I mean combine the two test methods into just this class
yeah that one all it's doing is saying we get this view name if there are search results but we're already doing that
we're just not checking the view name in that other test so I think we can basically copy the assertion put it in the
other one that that returns results there yeah uh we'll need to capture the view name from 48 and now uh delete that
space backlash there yeah crazy Fingers um and now let's delete the first test because we don't need it anymore hey we'
re deleting a test I was about to say that yay we're deleting a test don't that would be right safe delete yep yeah you
can do that yeah I was just wanted to try it uh so let's um let's just run the io free test because I think that's all
we point nice use of shortcuts all right uh let's Commit This what do we say here um so we updated uh the HTML to be
specific to its page so we can just say contents um and the controller uh so really the main thing is we're no longer
adding the the empty results attribute should we turn this into English rather than code no because this is a technical
thing so okay was it empty results I don't remember what it was called I don't know that's why I was yeah hey Carl nice
to see you uh are the exceptions defined in the test methods thrown by the code no um I generally and this is just my
preference um I often add a throws exception so that I don't have to worry about it if it if it does it's part of my
template I've gone back and forth about it um but that way if the code does throw an exception I don't have to add
anything to it because I'm generally if it does throw an exception and it's desired uh I will have an assertion for it
um if it doesn't and it throws an exception well all right um so let's run the application just take a look nope I need
to have this my little cheat sheet shortcut cheat sheet in a window covered oh it's still running from before yeah yeah
so my preference is I always want it to stop and rerun I never wanted to yeah I should just taking that would you ever
run it yeah that's would I ever run it without stopping no I I wouldn't that's my my don't all right let's let's go
bring up the seconds yeah let's refresh wait a second but isn't New Year's the only one we do have yes oh that's because
we didn't we haven't coded that yet so right now because it doesn't say no songs that's a successful page right so let's
do let's change the search to to yeah all right and now we get the not yeah sweet next step is to uh let's check let's
check jir where are we I think the jir I think we need to add some stuff in here so um we fixed that so let's go ahead
and and we can now reclose that uh now I think we're here yeah so um let's go right some more HTML or time Leaf based
HTML yeah want do another H2 um no I think we're just going to show a list so let's do um uh JW don't uh oh just is that
the word um perhaps yes please please call me on that I should have a I should have a just draw just like people have
swear jokes so let's uh o jira that's even worse no jir is the joke yeah see this is oira this file J that's that's our
that's our running gag in in this in this uh these series of episodes um so what we want to do is we want to iterate
through a list and so in th in the th Tim Leaf world uh what we're going to do is um let's we'll UL uh not uppercase
yeah you could do uppercase but it's an old old habit that's yeah um and what we want uh is to use a four um so let me
that one of these days I will publish my book um let's see so actually let's start out without uh we'll just use a p
that's repe was the context of one of these days I will publish my book um so I have I have a I have a book in in
progress that's been in progress for years uh which is a cookbook for time Leaf um time leaf recipes because one of the
things that I find um so there's some good books on time Leaf so wh de I don't know how to pronounce his name I'll post
the link in in chat has a couple of books on time Leaf but they are what I would consider sort of good depth but not I
want to for I I want to show a list of something how do I do it just give me the code um and my my my longin progress
book is exactly that uh you want a for Loop here you want a for loop with with radio buttons inside of a form here
because that's not straightforward at all uh you want checkbox instead of radio buttons here here's the code and just
copy and paste it so um uh yeah so I have to go actually since I haven't written a four each in time Leaf in more than a
few weeks I have to go and look at look at how to do it um so instead of an A List let's just do a bunch of paragraphs
because that's slightly easier so let's erase that uh so we'll open up a P tag and before we close the P each
interesting not Auto completing it did earlier uh that's weird um different we must have oh I know what happened we lost
our oh the Nam space just yes because intellig does this annoying thing where it cleans up unused name spaces and I'm
like stop freaking doing that so let's go copy it back from our haard results page no I think it's gone there too sorry
from my no results page oh is it gone from there too it's gone from both we deleted it in both remember all right well
then let's add it back here okay at least I kept the the the space for it uh so it is um that again NS no uh it's XML NS
colon th yeah we could look at the history and bring it back let's maybe let's do that thank thank you Carl want to do
that yeah let's do that so if you right just right click and uh local history uh that's fine and so go back a couple
yeah there we go and then you can just push it over that's much easier than typing it from scratch um actually let's
make sure we use it uh in this file otherwise it will tag um and we'll just put a th colon text and fine all 11 yeah
there we go uh so the way this works is this is this basically a for Loop um so we give it two pieces of information we
give it uh what will become the the basically the the VAR the local variable the index into the loop um and we'll just
call it song and then uh space and a colon in a space because I like to put spaces around the colon and then this is
where it's going to pull information from the template which is uh the dollar sign curly brace and inside there is going
to be the attrib rute in which we put the results so we'll have to go and check our look at our controller at the bottom
tag uh we could just do a th text of song so let's try that so still inside there yeah still all the th stuff is is an
attribute of oh another th tag yeah pH song y okay and let's just put a placeholder and just say placeholder song title
all right application where is your caps lock key that you keep hitting it I'm curious it's right yeah it's just it's
right above shift oh oh and so you're hitting it because you mean to hit shift yeah yeah I have my on on the Mac I've
got my caps lock mapped to holding equivalent to holding down every other meta key so it's basically all it's basically
command option control shift uh and the reason why is for some Global shortcuts um it's really handy to do that so I
just do caps lock and a key uh and it does years's interesting um oopsie uh but that worked um that's not yeah so I
forgot that that we're putting song view objects in it so what's inside of our song view maybe open that up at the
bottom there it is uh oh it's just title okay so uh what we can do is we can say where method so it's confusing because
the the spring expression language is very flexible and uh I don't know if for records it treats title without the PRS
we could try it um but we may as well call the method sort of doesn't matter right both both will work but technically
if you leave out the PRS it's treated as a property which means it looks for a getter um but since it's a record I think
that gets translated properly I'll have to do some res we could we could make sure we work with the PN and then just
undo it as a quick experiment find out yeah so let's uh application do not show this dialogue in you there actually is a
way with with Dev I don't I don't know if it requires Dev tools or not but there's a way to not have to restart the app
each time uh you can do a hard reload but restarting is more reliable all right there we go it's working yeah it's funny
seeing it in lowercase it's like that's weird that how you odd so technically we got jur 22 done um we do I wouldn't
mind showing multiple uh then let's go into the application and load up some multiple yeah I think we do we example let'
s see oh yeah we got this one now in the application itself we're just loading this one you can just copy top I'm not
grocking you mean copy this part uh well I was thinking copy the entire contents of that so you get the comma with it
yeah from there expand ah then so I would have done an expand there as well so you may yeah make sure theme sweet
awesome so let's commit uh let's let's let's close the J and then commit do this close J 22 oh okay it's pretty much
that J basically show show matching show matching results y do you want to put the ticket number uh we're showing no
results showing a different page with no results showing a um what else what are you thinking like what to do next yeah
um I'm also thinking can we check off the entire uh section from a generating the endpoint perspective yeah don't you
think yeah do um we could look back at our stories if we wanted I was thinking to take uh was it Carl or McGill I think
it was McGill's suggestion about pushing all the way to Pride ah um yeah so time for that can we do it and still have it
sort of I guess it would still be not visible to usually somebody knew the secret in yeah unless unless they were
watching the stream they wouldn't know what end point to hit yeah yeah so yeah what's so that means we want to do a
commit and push and then let me make sure my I have what is it co how do you pronounce that again K coab way when you
say it's still up what did you mean uh well at least the coab direct link is I'm not sure if you're do oh I see is is
forwarding correctly because I don't remember what the doc what I what the URL was yeah I gotta log back uh full nol
asks what about paging sorting what about paging and sorting uh we'll get there um those are those are forthcoming
features right now since we only have two songs and no way to add them uh we're not going to worry about that so right
now that's a yagy uh we don't need it right now but we will need point so I got Co B I'm logged in it looks like it's
still still running so really just to commit and push yeah let me um you can just do a push you don't have to do a
commit and push unless you want I mean it doesn't matter since we're just changing the jir yeah I fig might as well hey
do to attitude uh my database projects page and curses and be trees please help why are you writing a database because
you if you're using B trees that means you're writing a database which is a fun project uh I I of like that's a project
that's on my my eternal someday go right one of these things yeah cool I've written uh key value Stores um those are
those are fun um but you really really need to get stuff uh like be trees and so on there always a tutorial watch so
actually we could while we're waiting actually I can't you need to refresh um this website or does it keep you um as it
sees the push if you click on overview that's that's probably what we want because that'll show the activity there on
the right right and where it's provisioning so uh yeah so basically it's it's doing the deployment of the one you just
pushed got it luckily my um my real name is my screen name so I don't mind having my visible I wish I had a Jitter Ted
kind of cute handle but I don't know it has its ups and downs I think the upside is you can have uniform stuff
everywhere right that's true yeah yeah certainly unique absolutely yes like for Twitter my handle is at Rizzy because I
was on it so early I could just use my last name but you know other environments it's Mike rzy and other I have to
specify even more because there's more than one Mike rzy in the world okay so let's go to haven't looked at the website
in a while song thematic should look exactly the same and uh yeah so the source code is not public um it will be at some
point at some point it might be uh no promises made but uh basically it is our it's theme no I thought I needed to flash
uh so I haven't so I haven't like occasionally I will post on Twitter if there's something where uh I have no other way
of responding to someone um but I I don't post stuff on Twitter um I am on maedon so if you want to find me there uh
then and elsewhere ted. devout has all the links to Mastadon and Linkedin and so did I do it right oh wait a second I
wasn't checking to see it did it finish deploying oh it oh interesting let's drive in see we can happened uh oh it uh we
probably need something to tell it that it's running uh under Java 21 because by default it is not run under Java 21 I
thought we had done that but I thought we did that too yeah let's the um I forget what I forget what coab uses they they
they do it differently and probably what we'll want to do is um um just packages as a Docker file so we can so I finally
figured out how to how to do that and we'll probably want to add that because it's very annoying uh and it's kind of a
bummer that both coab and uh and Railway and some of these other really nice otherwise nice platforms of service um
Java's not a first class citizen Java is like like down on the list in fact on some of these types of platforms as a
service it doesn't even show up uh for well we did this in systemproperties um then in the pal oh yeah so we need to
change that to uh that Java runtime version to 21 that's why because it's possible that when we did this the the
original time 21 was not supported uh so sui yes we did get the the the growl VM compiled version to run uh but I did
not deploy it because uh we didn't get to the part where we put it inside of a container uh or at least put it inside of
a Docker file um when I pair with DeShawn next time that's that's on our list to do because I would like to use up a
mainly I'd like a faster startup sleep so if you click on where it says provisioning that link that'll show uh his
current status of building so we can happens and so it's interesting that that uh so coab is using uh the Heroku build
build packs um Railway uses NX packs but they haven't merged the update for to support recent Java uh I don't and I know
they had some technical reason why they want to use NX packs but that's why jaob is not ready there um and then there
are the cloud native build packs from uh from VMware um all stuff yeah I I'm also not sure when when we did it we had to
put this property that felt like a workaround that I'd like to understand why we had to specify that property what what
was in our what what's in ensembl that Gro didn't like uh is there some kind of what what was sort of being reflected or
something yeah yeah it's still it's still uh still with uh F asks uh how to be sure that our appc design respects cqs
principles so cqrs is not a principle uh and this is often what's confusing uh is um cqrs is is I don't know if I'd call
it an architecture everybody calls everything an architecture but it is a way of structuring uh and organizing your your
code in your system so we can call it an architecture so cqrs is uh command query responsibility segregation which I
wish was was had a different name because it's all about having um separate paths in your code for reads and for rights
and the reads are then eventually consistent with the rights uh often used with event sourcing but not but it doesn't
require to use event sourcing um the other way around is probably likely if you're going to use event sourcing you're
probably going to um cqs which is the original principle of command query separation uh all our domain objects should uh
adhere to that principle which is on your domain objects commands Our intention to change State and queries request
State and do not change State and that comes from berch and Meyer in the usk book oosc AR I would have gotten there
eventually want m m y r oh uh and it's from the from the usk book which is free if you want a copy of the usk book uh
which is objectoriented software construction uh beron Meyer uh has a has a has made it available for his a really
probably um it is a big book uh I think some of it's a little bit dated um but uh it's always uh interesting to to to
read a book like that but it is long this 1300 Pages it is a little bit of an academic text Booky like content uh but um
that's where it comes from um let good and have direct link do you okay while you're doing that I'm gonna check on in is
starting in is unhealthy I think uh it always starts out as unhealthy until it actually oh is up and running because
it's not yet responding yet uh yeah the plugin is nice if you if you want to if you don't want to have to rely on Docker
being available um then it's then it's really useful um I haven't tried it because I don't have I don't build my Docker
files uh I don't build my Docker files in the continuous integration I build them on the deployment uh yes that sounds
like a familiar growl VM issue I believe that was the one we hit and it had a suggestion of a property um so do you know
what that's know yeah so in if we said we want cqrs and how do we ensure that you might be able to enforce some of that
um by having clear separation in in whatever is writing into your database so if you're using the repository pattern
making it clear that only the right side not the right or left the the change State Side uh has access to the
transactional change data in your database uh and you could enforce that using something like Arc unit um you could
probably go even further than that and make sure that there are no methods in things that could write to the database um
I would wonder though there's a certain point of diminish turns on that because people can always write code to out with
static anal analyzers but if you want to do it just so that you don't do it accidentally you could you could probably
use ARC unit in combination with with that um that status looks healthy yep so it's rerun this woohoo all right we
pushed to production awesome thank you Mr Mill for the suggestion oh I'm not sure what's up with that sui I had Deshawn
walk me through that stuff so um pair with DeShawn he's always open pairing uh oh so was that a 32 so that was a 321
regression I guess um that's interesting yeah you can post link uh unlike YouTube twitch allows you to post links um JQ
assistant that feels a bit lower level than something like Arc unit uh Arc unit is really nice because it's much higher
level and and has some lots of good built-in rules um I always thought JQ system was a lower level kind scratch uh so
the one that enforces hexal architecture uh I don't think we have it in this project yet um but basically it uses Arc
unit so if you look at my ensembl project um I do have there H I'll check out that issue cool so it wasn't just me one
weird thing is is when we were when I was pairing with with DeShawn we ran into this Docker thing for the docker compos
uh not I don't know if you call it a plugin but the docker compos support and it was broken for both of us and recently
it just started working and I didn't change anything and that's one of those what what what got fixed is always a
concern um but all right um so I know we're we're a today let's let's yeah so let's figure out so we pushed to
production yay yep we did um uh what do we want to do we want to plan out anything for for next time yeah that well
technically it's our second push to production true we pushed actual we pushed new Behavior to production right yeah
that's the Italian spelling here we go um sorry I was just looking at the uh the link that that not pagas and by the way
I'm sorry I don't know how you want me to pronounce your username but um I was just looking at what was going on here so
it looks like it's a spring spr security problem um not a core spring spring framework so we've got searches for song
with one theme um so we could continue sort of on the read side as it were or the query side and search for multiple
themes or we could switch to the uh the right side the change State side and look at adding songs um or we could look at
uh persistence so I think those are those are the three directions we could go next I would say one of these two um I'm
kind of leaning towards this because then the more we do that it'll possibly inform persistence actually the other thing
that's for because right now we're just doing song title right yeah we gon have a lot of other attributes yes at what
point do we pull those in well th thinest vertical slice would be do adding songs do persistence then start adding
attribut if we wanted to get fully and and yes I'm thinking out loud here but yeah yeah so the the only downside to
delaying persistence is is again sort of how much do we want um that to influence the the architecture of the
application so uh right now the entire song database is uh is in memory right and we talked about this and it would be
perfectly fine to to do that forever right um but that means we're writing in a sense the indexing code uh but it will
be much faster um whether it's noticeably faster is a separate question uh but if we push some of that to the the
database um that will have an effect on things like when we search for multiple themes do we do that in memory or do we
rely on that that could be interesting experiment we could do when we at that you know somewhere around that point we
have enough data to see if it's perceptibly different yeah I wouldn't be thinking about it necessarily from from a from
a performance standpoint although it might be measurable but I but I doubt it um it'll be more how much do we want to
write that code and how much can we push off to something else uh and it would be right so I think somebody in the chat
was saying doing adding and persistence together versus as two separate approaches well so there's there's there's
adding songs from a UI from the UI which is I think what you mean by adding songs yeah um then there is persistence
which would require us to have internal code to add songs to persistence but would not require the UI right right
because when we start up so so like there on the bottom right in song themes application we're creating the song
Searcher and pre-populating with some songs um if we were using persistence we'd have to push that into we basically
have to store that in persistence unless it was is already there in which case we would do it um and that would only be
a bootstrapping uh we probably wouldn't application um we don't have to decide now sounds good I just got a call from or
my son is calling and I got the ringer turned off and but um so let's let's leave it yeah let's let's range from between
now and then yeah or let it mul yes marinate marinate right all right so that's all for for episode five thanks everyone
for joining and and as always thanks for the the great conversations in chat yeah um once Mike and I figure out the
schedule for next episodes we'll we'll announce that again best place to find that information if you want to know
before we actually start uh is always on on my Discord um because I announce it there and I'll announce the schedule
once we start planning it uh and I give you at least a little bit of a heads up when we're going to go live so that's
the be thanks everyone all right so thanks everyone and uh if we don't see you before the new year then have a good New
time
