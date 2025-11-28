# Upgrading Spring Boot 1.5 to 2.5 with Rewrite

**Video URL:** https://www.youtube.com/watch?v=r8lucJsNqRM

---

## Transcript

hi there my name is ted m young and uh this video uh is about a tool that i figured i'd try out and while i'm trying it
out record a video of me trying it out so there's a project called open rewrite uh that what it can do is uh rewrite
your code usually used for tasks like upgrading versions of your frameworks or your libraries and i decided to test it
on a project that i'm resurrecting for a class i'm teaching in java that happens to be java 1 8 or java 8. spring boot
1.5 and also j unit 4. so i figured instead of me manually doing it it's not a large project i could do it but i figured
i wanted to try out this open rewrite project while well i have actually a perfect project for that so uh i already made
sure that all the tests pass because i've got lots of tests um they all pass both from running inside intellij and
running from maven so just want to make sure maven was was all working as well so that's all good i already added the
plugin and so the next step is i'm going to run discover to tell me what recipes are available and we'll see and then
looks like i'll add in some configuration to tell it which recipes i actually want it to execute so let's go take a look
at what it comes up with so that's under uh maven plugins and i'm gonna do the discover one and so it looks like i can
do a bunch of different code styles i'm curious at how spring format v2 differs from this the google java format i'm
going to actually take a look at that but i'm not worried about styles right now i'm worried about the three things
which is upgrading java to 11 upgrading spring boot to 2.5 would be nice um as well as uh james knit four to g and u5 um
that latter one is actually the most interesting uh for for me because i want to be able to run tests under there's a
whole bunch of recipes so we've got uh some security that won't be interesting to look into there's a lot to want to
look into here some sort of standard things like if you want to change type or change package um looks like we could do
some of those some cleanup so things like maybe finalize local variables personally i dislike final local variables but
that's just me i prefer my methods to be small enough where i don't need it to be vital but i also don't work or no
longer work in a company that has a thousand developers working on a code base uh we've got format stuff around blank
lines and spaces and the wonderful tabs and indents stuff um maven properties so uh i'm not seeing offhand how to do um
one for the one i'm actually interested in so let's go take a look uh migrate to java let's do migrate to spring boot 2
from spring boot 1. let's take a look so what does this do it'll update the maven dependencies it'll migrate any spring
boot properties some wiring stuff and it'll do the june at four to five migration um so that is pretty much what i want
other than the the java 8 to 11 which uh i guess i can run separately so um how to do it it's showing me the before it's
showing me some conditional beam configuration i don't see actually how to execute this so let's um let's go to the
configuration so what i'm looking for is what the name of the recipe i want so i would have expected to see some spring
boot stuff so i'm not sure why because those should have come up first no so i wonder why i didn't i could generate that
but that's that's not not interesting because everything compiles under spring boot 1.5 so um and it's certainly at
least indirectly using junit 4. migrate so all right well i am a little stuck um because i would have expected it to
find it i did that i did the discover um but i don't know the name of the um oh so this is confusing if i understand
what this is saying correctly it's that there are recipes that are not part of rewrite core so if i'm going to need to
pull in uh rewrite spring which is what it looks like here as a dependency of the plugin let's try that so let's pull
that in and then what we'll do is we'll run the discover and see if that gives us anything in addition let intellij do
its thing um so i'm a bit iffy because it's unclear to me whether this got pulled in um intellij can be sometimes flaky
about uh whether it actually worked so let's let's do a discover and see if that made any difference aha so it is
pulling and yeah so we're seeing additional things like assert j and we're seeing spring boot stuff all right so um that
is an issue i will have to file or maybe just uh do a pull request directly for the documentation that when they do the
migrate to spring boot in fact i think both of these only well certainly the rewrite spring related stuff only showed up
when i added the rewrite spring recipe um that uh was sort of unexpected had i because i got stuck before basically
getting to this step and so i would not have realized that unless i unless i pushed forward um i think i just i went out
what i don't know is how much this recipe covers i assume that's this one so what i would do here is i would say uh and
here's the specific recipe that you're going to run because whereas i can tell that specific recipe is not mentioned
anywhere so let's try that um so the way we do that is we add on configuration active recipes so we'll put that here but
we don't want this recipe um what was it this one and uh hopefully that'll do everything it would be nice to see sort of
also um if there's some kind of relationship like does this recipe call sort of encompass several others that's what it
appears to be saying here so um be nice to also i wonder if i can configure it because i actually like the auto wired
annotation so we'll see what happens there all right um let's do a dry run because that was one of the options so let's
go do that uh let's open up maven rewrite do a dry run see what happens so it's running the recipe so clearly parsing
the palm which i would assume is going traversing all dependencies now it's running the recipes all right so what would
it change would so do no auto wired which all right and it would be running the junit 5 assert to assertions uh test
annotation test annotation runner to extension so that's another one so spring um changed it so you don't know you no
longer need the space sort of uh runner or extends with we'll see if it makes that change because turning it to an
extension from runner is not enough but we'll see and then the rest are actually just updating the test annotations
which is fine it would also upgrade the parent version presumably to two point something recent um and um we could look
at the patch but honestly um let's just run it so let's do let's do a commit so what it is i actually migrated from
gradle because i can't stand gradle migrated from and added open rewrite uh plug-in all right um yes please commit all
right so we've done we've done a commit so let's go rewrite run uh let's actually bring up some of these files let's go
to uh for example which one meal order api integration so let's go that one meal order api integration test that's this
one so presumably what it's going to do is it's going to replace the run with with extends extends extends with which in
spring what two two two three two four i don't remember one of those one of those uh it no you no longer need that
because that's part of the uh some other annotations but that's fine we can always remove that uh manually so um let's
bring up also we've got the pom file open so we can look at that ignore the redness here that's intellij not quite being
up to date all right let's go and then we can use the diff tool to see so yes as expected it changed this to extend with
so that's good although that's no longer needed because spring boot test now has that in there but that's fine redundant
is not a problem let's look at our pom file what did it upgrade spring to so it upgraded spring to the latest 2.5 which
was nice uh it did not update the java version so i think i'll have to run a separate migration for that or rewrite for
that but otherwise everything else looked good uh so we've got if we look at the imports so it it changed it to janet 5
jupiter pulled in that extension so let's let's do a rebuild and then we're gonna run the tests all right build
completed uh let's run aha so something's not right um let's see so we've got a null pointer exception here um so here
calling from this test sure cert certainly certainly should not uh cause a problem because we we built a meal um this is
a meal order kiosk thing just so you know what this is doing so we basically built an order that has a cheeseburger we
we set an id manually then we called a repository to save so i wonder what repository that is so that's an auto wired
one so that should be the real thing um uh in this case it's a fake one so when i say real thing i mean a real fake one
um that all seems fine so the question is why did we get a null uh i'll have to inspect that because all the other tests
pass so like this test passes which tests the repository um so it's possible there's some something that that changed in
some way with um because all these are failing so it looks like oh so the null pointer exception yeah i think it i think
rewrite made a mistake because i've got two constructors um this one is for tests this one is the one that's supposed to
be used by spring but because it dropped the auto wired i think spring is calling this one yeah so that's a bug in in
open rewrite so one thing i'll have to find out uh is when running a recipe can i sort of suppress some of the sort of
sub recipes like i'd like to run the migration from spring boot one to spring boot two but i wanted to not drop the auto
wired all right well that's comforting that it was something that was was that easy and wasn't sort of a deeper issue um
so let's uh let's do a commit and just look at all the differences we look at all the differences so these are probably
all around uh the junit migration just in this case just changing the junit 4 to j unit 5. so i've got a bunch of tests
so clearly it affected a bunch of tests this one same thing uh interesting i have i have this commented out because i
didn't want these tests to run so now this comment is wrong but that's no big deal i would not have expected open
rewrite to to do that um now it dropped so this is another thing that i know spring boot does for you uh if the id if
the name of the variable matches the path variable then it then you don't need to pass in the string um i don't trust it
because i'm refactoring all the time and doing renames all the time and i don't trust that uh to stay stable and i don't
trust that if i change this name here that it's always going to change this so i don't like that change um another test
change more tests changes um more test changes more tests uh and so here's where it looks like it it explicitly added
junit 5 which is actually not necessary because spring so so it excluded j unit 4 that's fine but we don't have to
explicitly include it uh anymore so that's another thing we'll have to file a an issue on now open rewrite is fairly
recent so i'm not surprised that you know there are these small things but in general this was this was nice more test
stuff i mean honestly just just the test stuff adjustment um and the fact that i didn't have to worry about i mean this
is not a sophisticated project but it's nice that it seemed to to handle most everything except for that dropping the
auto wired that it shouldn't it shouldn't have all right that's all for this video i hope uh you found this interesting
and you can find me on twitch where i do live coding so i do and you can also find me on twitter as jitterted so i'm
jitterted both on twitch on twitter and on youtube
