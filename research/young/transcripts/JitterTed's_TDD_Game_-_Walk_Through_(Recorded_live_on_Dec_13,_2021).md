# JitterTed's TDD Game - Walk Through (Recorded live on Dec 13, 2021)

**Video URL:** https://www.youtube.com/watch?v=p0cS11A5qrQ

---

## Transcript

so let's get started my name is ted m young jitter ted's tdd game is why we're here a little bit of of history of the
game i'm a teacher trainer coach been a software developer for decades but these days i am doing lots of training and
coaching and one of the things i teach is is test driven development and over the years as i've been sort of teaching it
and and doing it myself i basically refined it to sort of a 10 little step process so most of the time we you know
probably familiar with you know the the three-step process of red green refactor but sometime back i sort of really laid
out what is the the process that i actually follow and at least for the red green part it turns out to be this so i drew
this up several years ago and used this in in my training classes and one of the things that i wanted to do was just
find a way for for people to to remember the steps and so the original idea was just you know maybe i'll make each one
of these steps a card and then have people put them in the in the right order but when i looked at this i don't remember
if if it was me or somebody who's who had mentioned like hey that looks like a game board and it's like oh yeah i guess
so and so i did some early development and a friend of mine who's big into board games helped me do some of the original
sort of thinking about this and came up with some some prototypes and he and i played and you know we we did made some
cards and so made some cards like this and this and this and scribbled stuff out and so that was for the the origin of
it and we played it and revised it and and it turned out to be kind of fun like i my goal was not to to make a fun game
to be honest my goal was was to make something that would help people remember these these steps but over time it's like
hey this is act like as i was playing with my friends like hey this is actually kind of fun and and he said so and i'm
like really and so i decided to to further develop it and so the about gosh a couple of couple years ago now when we
could still meet in person i went to the agile open northwest conference and basically did some some tests plays there
and got some got some good feedback one person by the name of falco sort of found a way to slightly break the game so i
fixed i fixed that but in general got some good feedback made some revisions one of the original ideas is so let me let
me actually now show you show you the game so uh a couple of things one is the these hex cards this is from my original
prototype that i that i use for for play testing but i'll show what the print and play version looks like it's actually
much more in color so the center hexagon is is from the print and play version and some of these other cards and i'll
show show the hex cards basically they look like this so you can cut them out and there are different colors in
different different places and so as you can tell i'm a little bit of a fan of hexagons and so the the way the the game
works is you basically move through the steps that you would do to go through the full tdd cycle and so originally that
there were some cards and that were what i originally called sort of attack cards but after some playing i realized that
it's really not here it is so some of the attack cards are code bloats and can't assert and i'll go through sort of what
what these are uh and so originally the idea was as a two-player game you sort of played on somebody else's workspace
and so the idea is you pick cards and you go through cards and you end up with with cards in your workspace but it
turned out to be actually more interesting that when you hit one of these it was it was as if you found this problem in
your own code base and you had to deal with it so turn turn from attack cards to just tech debt cards and there's also
this idea of of risk that we take on if we skip certain steps so let me now sort of go through what what the game how
the game is played so as you can see there's there's hexagons and it's arranged in a certain order and with the print
and play version there's actually you have your sort of first task is to assemble the board and you have to figure out
in which or which order it goes in now there is a key to tell you how to how to lay it out properly but sort of part of
sort of part of the learning aspect of it is just get the board set up so that it's in uh the right order it tells you
here is the correct board setup you can sort of hide that and lay it out to make sure that you've put things in the
right order put the steps in the right order so the the way the game starts is so the basically your basic turn consists
of of dealing yourself and getting into your hand three cards so up here on the top i have sort of the print and play
version of the card so each card has the back of the card and then there are various actions and so these are from the
my prototype but it was just easy it's easier a little bit easier to handle with these so there's various cards and we'
ll walk through each each and so your your goal is is to basically go around and commit code without having to revert
and so if you have risk if you take on risk then by skipping certain steps such as writing tests or getting them to to
fail or or pass then then you have to revert and go back to step one and so when you're playing the two player game it's
basically whoever gets to to five commits first they they'll they're the winner if you're you can actually play this as
a solo game and it's just you know you can just play and and try out different different strategies but it's a lot more
fun with with two player i haven't tried it with with more than two players you just need more cards but it's certain
certainly possible to to play that way and so the way you go around the board is each hexagon has an exit criteria so in
order to basically get to the to the next card so i'm going to deal myself three cards and these cards it's open face so
you don't actually need to hide your cards so that makes it a little bit easier to to play and so if i get delt these
cards then my goal is to discard to move on to the next step and so a turn is basically playing or discarding three
cards from your hand so once you've done that then your turn is over you draw back to a full hand and then and then your
turn and then you're basically the next person goes so i'm gonna basically say all right i'm gonna discard one of the
right code cards so i'll discard that and then i'll move and so to exit this step so what should it do that's the first
step in test driven development how do you know what it's going to do and then the next step is how do you know uh it's
going to do it right so this is what kind of test are you going to write so that's for the thinking behind that and so
to exit from here we discard another card i'm going to discard the code for the less code card and then at this point i
can to exit i need to write code or i can skip to down here which is basically right write your feature code but i take
on risk and i take on a lot of risk here so i take on plus three risk and so if i did that i would have to say all right
my cycle risk is is now three and so for the print and play version one of the things you'll need to do is you'll need
to have some extra pieces like pawns to figure out you know who's where you'll need a six-sided random number generator
like a six-sided die is a good random number generator and you'll need something to keep track of your cycle risk your
code risk and your commits you can use little pieces of lego just don't step on them or you can use things from other
games and so if i decided you know what i'm gonna skip i'm gonna take on risk so that means your cycle risk is three and
that affects it when you when you go to commit that's where uh the randomness so i'm going to now discard this card and
take on three new cards and then and so now to so if it were two player the other player would go but now i'm going to
go on my next turn and so to exit here we need to write codes that means i need to basically play a right code card now
one of the things about writing code is writing code is good when we're doing test driven development but we also
sometimes write too much code and so one of the things about this this game is it has this test results aspect so if i
want to write code i may decide to to be safer i'm going to try and so i've written i've basically played a write code
in a less code card and i'm going to discard this this other write code card in order to exit i need to basically run my
tests but one of the key things about how i teach test driven development is this idea of prediction precise prediction
so when i'm doing tdd not only do i say i expect this to pass or fail it's i am very precise about how i expect it to to
well passes no precision needed there but when it fails i need to predict precisely how how it fails not just it's going
to fail but it's going to fail because it's calculating this and it should be three and not two as a currently so when
we want to exit from here we need to predict and so i play my predict card and that means i now pick a test results card
to see what happened and so if i pick this card it basically says if i have one or or no less code cards then it was an
unexpected test result and that happens sometimes you predict and the tests don't pass as expected and so in this case
if it's unexpected basically i don't go anywhere i don't get to leave so that card gets discarded and i have to try
again so i don't have any other predict cards so i'll discard those but i have another code co less code card so i'm
going to play that as well and so you can play up to two less code cards and that helps with it with then getting past
the test results so i'll deal my cards again my turn again i'm going to predict and now now that i've got two less code
cards this one says as predicted so your tests rat ran and matched your prediction so i get to exit so i can clean up
discard all my cards exit basically i discard my hands already did that now i took on some risk so i have to roll the
die so i can't i'm not safe yet and so if i roll a die it's basically if i roll more than the risk then its success and
so i rolled a six lucky me which was more than the three and i basically get to get to add a commit there now the thing
is i took on risk so that cycle risk doesn't go by itself it basically gets trans because i've now committed code where
i basically skipped a whole bunch of steps and so that risk stays there and affects the the commit opportunity next time
now there are ways so there's a refactor card which can basically reduce you reduce your your risk and so you can play
that it reduces your risk and then the refactor cards help reduce the risk you can take on risk by skipping steps the
tech debt cards and so there are two one of them is is code bloat this idea of your code is is too bloated and so if you
get that card it immediately affects you and so if you had written code but with a less code it basically gets rid of
one of them and so it acts as uh it makes your tests less predictable can't assert and so this basically means you get
stuck here because you're about to write code but you can't figure out how to write the assert and so you get stuck
there and the only way to get out of that is to basically skip a turn or if you happen to have a refactoring card that
always helps makes things easier to test so that's that's basically the the game and the instruction booklet sort of
talks about all that stuff in a little bit more more detail and the print and play version so these these are the hex
cards and that you lay out and then these are the individual cards and so what i use is these card sleeves you can use
the card sleeves just by themselves or you can sort of stick in a playing card to make it a little bit stiffer and you
print out basically as many as you need for for the number of players that you're playing with and so these are the
backs of the cards this is what it looks like if you print and we've got our other cards our predict cards our score
tracker cards the test results cards and the back of those although i'm going to revise this to not use so much orange
because i these were meant originally designed for printing on actual cards like i like i've done here in production but
i don't want to waste all your orange ink so i'm going to basically change the the background of those to not be so not
be so that's the game if you got any questions or thoughts i'm happy to answer those now but that was my intention is to
give you a little bit of a flavor of the game and and what the thank you my recollection's a little fuzzy but did you
you tweaked the the risk part of it where it's not loaded at the two two and the only way you get code risk is through
the cycle risk you don't directly ever bump the code risk up right the code risk the code risk comes only if the cycle
risk remains yeah yeah that was a tweak because it was it was again sort of like um well that risk doesn't really go
away at the end just because you committed and so so wanted to give it give a little bit of a flavor of that because
otherwise people would like oh i'm just going to really take on risk all the time and it has no effect on the future and
i want to inject a little bit of that flavor so yeah all right any other any other questions or thoughts so the the
print and play files i'm finalizing them and basically probably by the end of the day they'll be made available for
those of you who bought and i know some of you already did and i really appreciate that i mean i've for a long time
wanted to get the production printed versions in but there was a little bit there was some stuff that i wasn't quite
thrilled with but i figured you know what done is and out there is better than perfect so thanks for seeing it that way
yeah and and for those who who nagged me sorry about that but but thanks for nagging so i will be putting i actually am
going to have someone do some cleanup on this for for getting them actually into production i've already the game
crafter setup is is almost is almost done so probably january february time frame is when i'll have some initial copies
actually of the physical product to to offer and you'll get a credit of probably most of the money you spent on the
print and play if you bought the print and play against the the physical version so don't feel like it's it's you won't
get any benefit from that and this is you know this has been play tested you know a dozen times but it doesn't mean it's
it's perfect or it's there yet so if when you get it if you have any feedback or any comments don't hesitate to let me
know and if you buy the print and play you'll get all revisions as as i as i all right that's that's all i had for you
and so i really appreciate your your support and and the time spent on looking this over and i'll look forward to to
getting feedback from playing the game thank you ted all right thanks joel thanks everyone i really think that this
technique of tdd is powerful and yet hard for certain people to pick up yeah if if this can help those people like some
people it just made sense and they started doing it but another group that hasn't if this can help you know be the
gateway to them doing it you're you're doing a good thing for humanity yeah i mean and and i hope and i hope people like
you know i i teach this and i also uh do learning ensembles or mod programming and it's it's just fascinating how easy
it is to hit the run button on the test without saying how do i think this is going to fail and then it fails and fails
for the wrong reason and they don't realize it and then they move on with with basically an incorrect assumption and so
yeah so if we can just get them that then yes i will consider this a wild success so all right all right that's all
folks thank you so much and i'll i'll see you around the the internets bye
