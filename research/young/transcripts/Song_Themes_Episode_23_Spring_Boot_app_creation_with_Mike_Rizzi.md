# ＂Song Themes＂ Episode 23： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=cDG8KvqWVcY

---

## Transcript

that all right hello folks good morning good afternoon good evening welcome to another pairing stream how you doing this
morning Mike doing good doing good A little bit of a froggy voice that'll come and go but other than that doing right so
uh what we've been working on is the song themes app and we've been spending time on uh making the import process easier
and um one thing I was I was thinking about was like we're we're probably doing work that is done by a library um
especially sort of matching up headers and things like that oh yeah um what are what are your what are your thoughts I
mean we could basically say why don't we just find a library that does this uh sort of matching up the columns with with
the data uh and then just extracting that versus um continuing uh down that road of of doing ourselves I could go either
way I mean my initial inclination is let's code it up and then see if there's a library and then decide is a library
such that we don't need the code or if we just go down the path where this coding this up is turning out to be a lot
more work where we're going down the not invented here syndrome right path where it's like okay this is gnarlier than we
thought it was let's just steal from someone else I mean borrow yeah and so um what were you thinking hey there veganes
uh I I I wasn't think I mean you know it's what is what is our purpose um and how much effort is it uh to to to do it
ourselves because I I don't think it's a whole lot of effort I mean um in terms of lines of code or or any kind of
measurement you know related to to sort of how much work it is uh you know but it also depends on like you know what's
what's our goal um how long will it take us to to to find an appropriate library and then use it and then integrate it
and then we've now got a dependency although something like this is going to be fairly stable it's not like it's gonna
you know dependencies are going to update very frequently things like that so right um it's it's really more what is you
know our goal here on on the stream right so that's what there are several I guess right there's one where we want to
build this app right two we want to practice in some things we maybe haven't done or I haven't done um like I've never
done this sort of bulk import kind of stuff before so this is kind of a gas um that's positive slang by the way um and
then you know the folks watching you know is it helpful for them to see uh right I'm inclined to keep going with hand
rolling it okay until we get into a major speed bump is sort of my gut and then then we go oh I guess it's harder to
build that trust Tower than we thought it was you know yeah I mean certainly from um sort of a learning practice point
of view it's it's obviously better to to to build it ourselves um and uh so I'm I'm fine with with continuing down down
that route I just wanted to sort of check in and and make sure that you know we're not we're not going into this without
thinking about you know alter Alternatives no it's good I'm glad you raised it did you look at all into to seeing if
there any that exist oh yeah there there there are a bunch um many of them are are uh I mean there there are lots of
them and so part of the the issue is is sort of selecting which one we want to use and um I have to go back to to ones I
originally found and uh again it's sort of like that's effort on it that's yeah that's that's its own you know what's
what's the cost of pulling in this dependency if it's because a lot of these libraries because their libraries tend to
to be as is their nature sort of overly I don't know if complex is the right word but handle many more cases than we
need to handle right um so yeah but let's uh let's continue down the road and let's let's see where we we left off
sounds good bring up your screen a second problem give me time to move the uh stre out of the way all right there we go
I really want to get my monitors stocked one above the other instead of side to side because I here okay I'm on all my
monitors right here except you can't do that unless unless you're wearing like a Vision Pro and then you you got the
different things going on maybe that would be the actual use for those clear monitors did you see one of those where
there it's like a piece of glass well make maybe you could sort of somehow switch one off so it's just clear and you
could see to the one behind it and then I don't know I can't really see a use for a piece of glass monitor at this point
um at least from my but we got a failing test um I do not remember where we left off but apparently it was related to
that yeah so what we did was um uh if we look at the song uh song service test I think the ones that's failing there um
actually I think they're all failing for the same reason which is we we we basically tried uh what if we said the uh the
minimal columns were were three so if we look at the the parser itself we'll see that's where um I think if you yeah so
we we basically set the minimum colums to three because really the minimum columns um of required columns is actually
three because it's artist song title and and at least one theme right um but by doing that we basically broke uh we we
broke a bunch so you think look at them one at a time top down or I think if we look at yeah if we go straight to the
yellow Amber whatever color that is uh is failing sort of for for a different reason than the others because here it
doesn't have enough and sort of expected that uh this one would fail um why don't we uh change minimum columns back to I
think it was eight before or nine whatever it was before uh and let's run the run the test again so now only one should
right so we'll make this one pass and then then move to the moving the minimum columns back to or not back to but to the
correct number yeah so this is this is where where we ran into the problems like in order for this test this test should
pass um but it doesn't have the minimum number of columns right but if we change the minimum number of columns as we
just saw uh we break a bunch of other things so is there a smaller step we can take that lets this one work um or you
know because to disable this and change minimum columns to three and then tests because right I mean the goal is three
so it means the other tests are checking something likely checking something yeah so maybe let's change it to three see
see what the tests uh see which tests are failing and and and how much work it's going to be to to fix them up yeah uh
um one thing I would do for from a formatting standpoint is put the on line 55 there at the end put the triple quotes on
a new line 55 oh like that um then reformat yeah if you reformat I'm not sure it might just leave it I'm not sure go
ahead and reformat ah good that did what I thought hoped it would do it's kind of weird to have this or do you normally
like that offset uh I don't care about the offset it's whatever the fal you could try to unindent it um I guess I'm not
sure that's much better so maybe let's let's go back or I mean to me this is yeah slightly better um yeah the question
is will the auto reform so there is a setting that I've changed on on how it does text blocks because I find that it's
default uh setting is B something like that and I don't understand I understand why but I don't I don't like it um all
right let's let's not sorry for distracting not yak shave on that yeah so this is failing because um where is it
actually failing it's failing on song ah okay so this is this is this is interesting so it's failing in a different
place um oh because this one is expecting four columns yeah so what we what we what we did was uh we handle if it if it
didn't have enough columns right so basically preventing the exception that we just got which is uh there aren't three
columns or there isn't a column uh three from zerob based um so when we change the minimum our guard Clause no longer
issue uh so what we can do um is we can we can fix that we can required so we check if there is a fourth element and if
there is release type or uh actually let's let's think a bit deeper um is the test still correct let's go back let me
make it bigger because it's kind of a large test so we do a a create tsv song with header but the data doesn't match the
headers and the header may not be correct either so I think the the intention of the test is just that we get failure
messages for a failed import but I think our test data is no longer something expect but we're expecting a failure in
this case because line 57 is only two right we're expecting two failures right because line 57 only has two columns and
line 58 uh only has three columns so we're expecting two failures right in the current test in in this test um yes but
it's that's not that's not like that would never that could that could that would be difficult data to to uh to import
like you wouldn't be able to copy a spreadsheet in such a way that You' get that data good point so um so I think this
now but we still want an a failure message for a failed import we need the failed we need we need we need the failure to
be a reasonable failure as completely not I won't say impossible the H one of my favorite songs really yeah such a great
album album now alj is that what you're trying to do yeah that's what I was gonna do I was just double cheing because I
I one hey Desa AKA Java Grant how you doing and I popped up uh Mo M Mo before howy welcome welcome howy so let's see now
this is three songs I'm sorry three Fields right but the header doesn't match but the header doesn't match so what I
would say is um import this method and then let's clean up the the header to to match when you say import you mean
inline I'm sorry inline yes okay not sure not sure why I said import well we are working with the song importer that's
true uh and I had to inline the variable so we can actually or maybe just copy and paste it which variable uh for the
for the header oh like this got it that's what you meant yeah and so what we've got we've got artist song title release
title uh so then let's get headers oh wait yeah but the required is four which means a theme oh but this is a failure
this is a failure yeah but do we want to leave theme as a header though or no because what we're trying to do is is oh
right simulate you only copy the first three columns because you only copy some reason yeah yeah um so if you if you
take that string and put it on line 54 and a half we can get rid of the the weird uh appending and mean just manually do
it or is there okay uh you'll need one more trip one more quot double quote oh there we go and uh it has to be on a new
line and now you've got to one too many because intellig was trying to be helpful where' that one come from yeah okay so
now we have valid invalid data um and this is really interesting because uh when you're doing tdd or any kind of where
you're writing tests on a regular basis you're going to have tests that no longer make sense when functionality needs to
change um and that's a fact of life uh and and people who don't like to write tests or maybe aren't very good at it um
tend to say oh see I told you now we got to do extra work now now do I not only have to change my code but now I have to
change my tests I like yes if you'd like that code to be correct then yes um it it is it could be considered sort of
wasteful overhead by folks who who uh don't like don't like the test as much um but then you may as well just delete the
test and say okay now we're not going to test this at all it's like that's that's your choice uh so um but in this case
especially when you're making functional changes like we are it's not just a matter of how do we make this test pass but
does this test still Mak sense in in the new world that we want and so before it didn't uh before it totally made sense
because we were just you know saying well we're going to cash the failures because there aren't enough columns but now
we're we're in a sense relaxing that requirement um to provide more flexibility as as we increase sort of the the the
complexity of the implementation uh which means we have to work uh change a copy of the test first no I I think we want
um what we want are tests that will continue to fail in the same way even with without changing the code to sort of
prepare for um our our new world uh as it were um in some cases it might make sense to basically say well let's let's
just actually delete the old test and and maybe it's as a whole it doesn't make any more sense uh doesn't make sense
anymore but this one does all all we're really doing uh and it's it's very easy to to get caught up and like you know
let's let's fix the you know the code to make this test pass but I guess when I'm saying in in a in a very long ways is
evaluate like does the test make sense and and can you change it to fit with the new uh the the new behavior that you're
going to want so I think this this is what we want we want to say you've only copied three columns from your happens and
I apologize for the car alarm if you can hear it is that what that is yes wow that's one loud car alarm well car alarms
are supposed to be loud even though nobody cares about them so um let's run just this test uh it should still fail
because it's it's got three columns but we're going to try to parse a fourth one but it's supposed to fail with two but
it's supposed to fail in a in a nice way as opposed to throwing an exception right so the nice way is basically return
uh failure failure results yeah yeah so still throwing the exception yeah so um so what can we do then to make this fail
in the right way with because it is it should have failure messages it should fail uh and it should fail with with a
result being not successful uh so what do we think we can we can do and while you think about that I'm going to go see
if I can shut some windows so we don't hear a car alarm yeah it's not his car alarm it's somebody else's I think he's
closing the place finally it timed out I believe there's a law that the alarms have to time out after a certain amount
of time so seems like that one my car is so old I actually makes it more valuable but car so um what do we want to do
where is that being thrown oh it's being thrown from here ah yeah because we're we're accessing the fourth column which
is column three which does not exist which does not exist so is there a way to test if it exists and if it does assign
it to a lead type otherwise ignore or do we do the simplest thing that could work and just make don't don't grab release
type just yet um I would say Let's uh let's return a result a failure result if we try to access this column and it
doesn't exist the other opt the the other option is we change the minimum columns to four so this doesn't happen uh and
I wonder actually I wonder what that looks like let's try that first experiment first yeah yeah now run all tests yeah
or all I free yeah we reduce the number of test failing by quite a few yep um I'm wondering if if we should see if we
can get it to work get these two tests to work and then go back issue yeah let's let's take a look at these so this one
so let's I would probably say the single song is since it's at the sort of the lowest level uh do um I mean this is the
simplest one to change would say okay well four is our our new minimum so then it should just say four right now what's
interesting is it's showing it's showing the two columns that it has but it has more than two no no that's not the test
that's fail it oh ah what are you thinking I was seeing if there was the uh the side by side compare that wasn't there
so we could just do that yeah yeah that's our that's our our new Behavior we're we're we're allowing uh fewer fewer
columns because really we should never have not never but uh it perhaps was not correct to to force it to be nine
columns now this is Ping parsing a single song at this point do we say we shouldn't even be passing in the test to or do
we get this to Green first and then deal with that I think get the green and then we can re-evaluate uh uh where where
we're at okay so that one went went to one so this is the one that should be success UC f um but isn't yet return
success when hit rule has required columns so we got so this is this is the test that we'd like that ultimately that we'
d like to get passing but uh there's here so I don't think there's any way to get this test to pass without changing the
minimum required columns to three to three yeah I which will of course Cascade and cause the other tests to fail that's
fine we can then look at the other tests and see so make it three we haven't actually committed in a while I was just
thinking um well everything's breaking now yeah yeah I don't know that there's much to commit yeah we haven't other than
writing the test on top we haven't done a lot so I I think these are all going to fail because index three out of bounds
for for length of three um which is always such a confusing error message unless you unless you understand that oh
you're saying index zerob based index Three is out of range um so let's uh let's I think let's do some backwards
compatible uh change which is um if there isn't a third column I think if we make that change so that uh if if there
isn't that that fourth column uh index three then we return a failure message um and then we then we then we'll be at we
should be at pretty much passing test and we can actually start changing the functionality to support this this test so
um I'd actually say let's disable the test on top because we're it uh and I would actually put sort of in peren a
comment a string that says um enable when ready to functionality changing functionality is kind of vague do we want to
be a little more specific or is note I I I don't think yeah which one do we want to tackle first um I would I would say
the the lowest level one so rerun the test song uh so that one's failing because because of the we can probably update
that one um to just say must have at least three because that's that's now go it I wish there was something in between
150% and uh Zoom what Zoom are you at uh 150 Oh I thought we agreed 125 was sufficient I thought that was did we do that
for here or for ensembling um I'm not sure okay yeah my notes still say for setup 150 no I think 125 125 okay let me
change my my setup notes well our viewers can tell us if if this current zoom level is okay uh because it looks okay to
me um so but people can tell us yeah the text is too small at us now yeah well so there's a difference between like and
and can read so uh if you can't read it then that's a problem but if it's just a preference but you can still read it
then weightly trying to get screen yeah we're we're going to optimize for for bounds right so the I'm going to apply the
the the question again does the test on top make sense and those RS with not enough columns no because yeah it doesn't
make sense at all in fact I feel like we've already got a test like this the one where we import uh in inline the header
right so we can just blow this test away I think we can uh so this one is yeah because that one was testing failure
messages this one was just is just testing that it fails but I think the other one supersedes this one so again hey
there stend is follow um Define big so you're asking do I know of any big open source Java projects with good uh but I
you know because I can refer you to a bunch of projects but I don't know what big means um I will say that uh I don't
know of any that are let's let's say bigger than the projects that that I work on on streams um and I've looked a lot uh
mainly because there are simply not not very many open-source applications lots and lots of Open Source libraries and
tools and things like that but very few relatively uh actual applications and the ones that I've looked at are poorly
organized or or insufficiently tested um but if you all find good ones let me know because I'm constantly on the lookout
for them but uh open source is skewed towards libraries and and Frameworks and tools and utilities and things like that
and there's very few full-fledged app applications that that are like enduser applications as opposed to things oriented
at at developers there are some Point of Sales Systems survey tools um and the ones I found in in in Java are great for
me because they're bad examples of of stuff um so I can certainly offer you bad examples but uh non-trivial applications
that are well lot hey there the Zero official are there any public projects with good architecture um not that I'm aware
of there there may be some uh I the problem is is when they get big um The open- Source ones they again they sort of
there aren't a lot of so projects yes welcome all right so um what are our failing tests now the one on the top screen
okay uh index out of bounds all right well then let's make that one well does that help us or does that make yeah so
that's a step in the wrong direction because we've now broken other tests yeah I would I would say undo that nice to
experiment but that that's a step that that takes us away from from our goal so what is the the test on the top
expecting two failure messages not an exception Throne well redirect a song import two failure messages and the songs Do
we have a failure test in the in the tsv song parser because this is right so we've got like a couple of failures but we
don't have um what's this the second one partial all returns failure when missing required yeah so we haven't yet yeah
so that's the one about the so um we may have deleted the the the closer in test that actually tests uh our our failure
messages I was wondering about that the one we just delited yeah it was it was insufficient um and I thought we were
actually testing the failure are we actually testing failure M so we are testing failure messages in the test above the
one you're currently showing so that one says Parc all returns failure when fewer than two rows but do we have one that
uh does parsall failures so what I would search for is is just look for result. failure class so that one uh returns a
single failure message y single that one is about right so so there's sort of two dimensions of of error messages
failure messages there's this row is wrong uh which was the other one and this one which is the entire import is wrong
right um do we are those the only two that actually test for yep yeah only those two um so I would say we probably want
a test that has multiple failure messages so similar to this test and we could even expand this test um oh this is par
single song so it's a lower yeah this is par single song so we actually don't have one that's testing failure messages
uh on a on a rowby row basis so we need to basically do that and we could probably copy the test from the song importer
test and and and sort of retarget it because it's got a good yeah basically just take take our setup from here uh of
just the string because everything else we don't need okay just and we want to do this at the song level or at the parol
level uh at the parel because what we want is what we're missing is a test that um gives us multiple failure results we
don't currently have a test for multiple failure results um something like that uh I yeah so parcel returns messages
yeah I think that's fine good enough okay yeah you've got the search turned on which is causing the highlighting so you
can escape out of that yeah yeah I'm not sure number of commits dependents follow is is a good is a good metric um I
think you'd want uh a metric of really of of size of codebase um because I can I can give you a a you know a three class
project that's been committed lots of times then that's not going to probably be useful because my guess is you're
looking for for a project like you said uh you know if if it's going to have an architecture and it's going to have DDD
in tests it's likely going to be of a certain size um so uh honestly the projects I recommend are mine uh uh so ensembl
is a is is a real world project it's not huge um but it's definitely DDD it's definitely hexagonal it's definitely lots
of tests because it was test driven um so that's usually usually what I recommend uh it's it's it's non-trivial but it's
but it is I wouldn't call it Big um I would say it's still a small siiz project um but again that's why I ask biggest
like biggest relatives like uh I I always joke it's like whenever a bunch of Runners get together um and somebody says
yeah I'm a slow Runner I say well what does that mean to you it's like yeah I only run eight minute miles and I'm like
okay the fastest I can run the fastest I can run is is 9 minute miles so clearly you are not slow um using number using
things that are that are uh descriptors instead of numbers uh problematic plus as Einstein said Everything's Relative
yes where's that Rim shot when you need it yeah exactly um I've done I think what we want to do is yeah so I think
before that we just want to say has sizea two uh and then we you can keep that it'll fail on the has two oh and you can
chain them like this yep a well she use the right the right test uh do you want to predict before we uh let it rip or
character I think it's going to throw the exception right yeah y so what we'd like to do is is make we want this not to
blow up right but we message so here this method is ending with a result success in all scenarios right except at the
guard Clause right so would we have another guard before we even get to 71 that then returns a failure result yeah why
not let's try it something like U and would just be really specific I mean how do you test if a column exists in index
has length is length the number of columns or number of array elements yeah the question is is is this going to do us
any good um right because we just checked for four we just checked for four if we check for three here it's gonna break
we're back right why do I feel like we're in to catch um so let's so here we expect failure why do we expect failure
because we don't have uh the required columns even though we have enough columns oh because we're not checking the
headers yeah one right so this is giving us so so let's make this test pass and we can just pretty much copy the output
because the output is for now going to be going to be fine we can just literally copy those the actual everything in
inside the the quotes oh all the way yeah you want to yeah and then basically just paste that into the so it was a bit
of a characterization test but that's pass wrote uh so where are we now if we run all the tests I think everything
passed uh you're not running all the tests oh all you meaning I mean it's forgot uh yeah that one just keeps flipping
back and forth um technically uh well let's change it let's get to to passing um and then I think we we've got to start
uh yeah so so this is probably a good commit uh did the stream start earlier today no started at the usual time um but
if you're in a time zone outside of the US then you might be off by uh because of a time zone change um but we started
at the announced time which was 9:30 Pacific UTC so I think that's the main thing is we basically reduced the number of
required four maybe don't need to say what we're yeah all right so I I think um we can now go and look at at our
disabled test because I think now we have to actually start change changing functionality which one we've got two uh
well the first one is not really written yet so it's the second one that we want right the first one's empty yeah so
let's let's delete the fail feel like we need to put the result is success is true first before we check for failure
messages empty it feels weird to check the success last that is that oh maybe we were growing the code and we were
starting yeah so all I know about cotland V is is long build longer build times than Java um that's why I don't use
cotlin uh I slow see the same reason I don't like typescript because it's slow um compiling Java isn't immediate unlike
you know a non-compounded language like JavaScript um but it's usually fast enough and and development environments have
been optimized for for uh and build tools have been optimized for rebuilding uh pretty quickly so say uh what are what
are our tests against the the parse song method the I think there's only one yeah the one that's in the nested test
class but not Nest this yeah so here because uh so this returns failure for row with not enough columns um again we can
sort of go we can we can do this inside out or outside in um we can either change par song directly uh or we can change
um it it basically will change it anyway but parol so you're saying have a new test at this level we're going to go
closer to Parson yeah so that that's that's one option is basically have have a test directly against parong um and this
is where we're going to have to pass in uh some kind of of schema or or just the head of rows and let it do it um this
is this is because it's currently hardcoded to use column indexes and we'd like it to stop doing that right so it makes
sense to do it here since we're really going to be modifying parong pretty dramatically uh we should probably write a
success a successful test and then uh and then modify it yeah so in a sense sort of should that that would that would
work right we want to mimic the title so it's like that um I would probably rephrase it to say with required columns ah
yeah it's true we gotta move to required because it's no longer the number right we've changed yeah yeah that's a very
good point should we rename this one or that number uh once we once we actually start changing Behavior then then we can
we sense so pretty much scale this and then change it to legit do I legit from another test in the class yeah I was
gonna do that the this blue oyster in here yeah this one because that's one with three uh but that's not correct what we
want one is one that's correct so it has the required columns those are not the required columns oh right the card a
theme do we have one in this yeah that one right there there we yeah well you're going to need eventually you're going
to you're going to need 54 um but that's fine we can yeah and so we want to drop the header um so i' probably just
comment me out shortly y That's it okay yeah and so now you can now you can say uh disabled until the parse single song
tests work uh so tsv stands for tab separated values as opposed to comma separated that's what tsv is I learned that a
little while ago myself for a while there we were naming columns yeah t tsv is is less common um which is strange
because it's such a better format um although it does use whites space so I guess from some points of view it might be a
worse format um with commas separated though you have to deal with commas actually in your data and that's the big
difference yeah yeah and the reason we're using tab separated is when we discovered we thought that when you copy from
an Excel spreadsheet like this that the default was comma separated or you had control over it turns out you have no
control in Excel and that it Gives You tab separated period end of story well I think we were originally thinking if you
if you exported it out of the CSV it would do the right thing with uh quoted comma which it doesn't it does which is
only for the sell yeah so it's inconsistent which made yeah doesn't it doesn't abide by the standard the the RFC
standard so it's it's useless um but then we also said well actually that's not what we want anyway we want to be able
to just copy and paste from the spreadsheet and that's when we discovered that it puts tabs in the clipboard which is
great um because that's easier all around yeah exactly okay um so I disabled that I can't remember if I reran the test
I'll just rerun them again CS are otherwise words for those of us who who tab indent our code I don't tab indent my code
yet I I have been toy with the idea of switching um so this fails for the right reason yeah it's basically failing even
though we'd like it to succeed um can we we've been a little bit lazy uh about um improving our test outputs so here it
just says expected value to be true but was false and that's not a very helpful uh failure bit do you know how to do
that or do you need help I think I need help um okay uh so if you put in 178 and a halfes uh uh and you say do as and
then we can put a string in there um song with minimal columns should have parsed successfully required Comm columns
yeah man my typing is CRA today with required columns is what was that again uh should have not period so now if we run
it it will it will at least show that message that's cool is that an assert that feature yeah yep nice yeah so I don't I
don't use the as for for when the output is clear what happened but when it's that If Only They had instead of is true
they had an is true it's overwritten where you could here so the discussion of that and it turned out to be confusing
what the message should say because is that message shown when it succeeds yeah yeah yeah um so yeah uh those kinds of
things can can seem obvious and then you try it out and it's like oh wait that's really confusing yeah so cool all right
um what I did wish it did and it can but it's hard uh is display the variable that you're assert asserting on um but
that's that's that's not easy oh assert on song result yeah and this is and this is where I tend I I I start looking at
and we've talked about this before uh creating a custom result assertion um and that would obviate the need for having
the as because then you'd say um assert song result is success and then it could Clearly say that it was uh successful
or failure and have a much better error message can song result be a parameter in other words can this be parameterized
in some way yeah you could you could um not uh not that necessarily that syntax but um I forget what the syntax it uses
for that uh would that help in what you were thinking of no what I was thinking of is is I don't want to have to write
that um because it's basic we're basically saying this this failed but should have succeeded right so We're translating
true and false to success and failure but result already understands success and failure so what I want is assert that
song result is Success right and then song result knows what the definition of what the what kind of failure it is and
it well it still wouldn't say that anything about required columns but it would just say that it's success and failure
at least using the language of the result instead of true and false instead of just a generic Boolean true it all right
um so this fails fails for the right reason um do we want to take a break before we embark on on making it pass yeah we
should it's been an hour y all right so we'll take a a a short break and then when we come back we will try to get take
some steps towards getting this test to pass so we'll see you in a bit see you for e so just a couple of notes um let's
see where are we yes uh so I have a Discord in case you didn't already know and if you didn't already know you're
welcome to join uh and it's a a nice Community for asking questions and discussing things um maybe you need some help
with a project you're working on uh or you want to discuss some thoughts or ideas about domain driven design or test
driven development or just testing in general um uh or things around intellig or um those those kinds of things like the
spring framework so all that we got channels for each one of those topics uh and lots of folks who are uh interested in
discussing them so go ahead and join go to ted. deev Discord and uh go ahead right so we left off that this had failed
we're wunning a test that we want to succeed yes so we'd like we'd like this to succeed um and we know we can't just
change the number of minimum columns because we know that causes others things to do uh um should we do a parallel
change to a different version of Parson well so uh we could so you had a little experiment where you basically replace
release type with an empty string and that broke things but maybe what we can do instead is actually only replace it
with an empty string if the if that column sub3 doesn't exist right and just do it it not be a failure message in other
words something like right so would you test if it doesn't exist by seeing if the length so if yeah we would evaluate
the length because there's no other way to do it other than catching an exception which is not a great way to do it is
less than three three well I would I would actually say well I don't know what you're going to put inside the if
statement um right so what I would say is if the columns length is greater than three assign it the way you have it on
that line uh yeah and so uh we need to bring release type into out of that scope so else um we need to bring that into
Enter uh so we want to split into declaration and assignment up and now we can do the else uh in fact we don't even need
to do the else we can there is that copesthetic well so intell is telling us something um because we now have minimum
Columns of four uh but I think we can now drop the three would you do that if um after testing to to see if this passes
and then move the minimum columns down well there's no possible way it could get to this line of code right without it
without their already being the that number of column right so if we ran this it would still fail right so if you look
at what intelligence telling us is that condition is always true yeah so if I go here yeah um but what we want is now
this allows us to change the minimum columns back down to three which is the true number of minimum columns and are we
just going to run this test or run all no we're going to okay so now they're breaking now they're breaking for a
different reason right um because we're trying to to parse uh themes so this one failing yes because we're not we're not
yet so how do we get back to green because we're not in a good state right now no um part of me thinks just revert this
because I'm not sure that's the The Next Step that work will work for us well if we revert it we keep going back to
stuff not working I think we need to push forward so I think what we need to do is we don't parse the themes if there
aren't at least uh a sufficient number of columns so the same thing that we did here is provided default if there
weren't more than three columns we provided def default uh of of uh of the themes if there's not enough columns so in
other words break this into um do exactly what we did for the other for for the release type is if if there's not enough
columns then provide a default so split into declaration yep so there's another way you could do that you could surround
it with an if split or maybe uh when you say surround meaning never mind never mind never mind no you can do it but I'm
not going to is it not I'm not going to bother telling walking you through it because it's it's actually more work so
just okay sounds good it's not work if you're really fluent but it's more work if I have to describe it so right got it
um new array list for an empty um no we just need to assign a an empty right collections empty w got it yeah and now we
can surround the parse themes yeah yeah so as long as it's got that one then it's it means it's at least that one and
then possibly more correct yeah so then this should this should get us back to to Green close to Green it may be that
the themes are wrong in some cases um but that's fine because we're succeeding now where we where perhaps we're needing
to fail right this is succeeding now so just go top down or do you want to go um up uh let's fix that one that one's
just an error message so we can just fix that one or a failure message good evening ASD so that one's got a redirect
unexpected this one's got a failure expecting false for expecting true same here tighter in first um so now what we need
to do is these are correct failures and we now need to uh basically correct for them um so we want what these are
expecting are failure messages because they are actually failures um and so what we want to do is update our code so
that if there aren't enough so having default themes is not what we want what we want is to just result sorry I'm lost
you may so this is a correct this test should fail but it's not in the sense of it it should be it should be it should
not be successful um but it is because and we can't tell so why don't we improve our error message there on 43 on the
assertion so let's run it again we message yeah so it should not have succeeded but it did and that's what we want to we
want to change so this is this is uh so the test is correct it's doing the right thing and now we need to change our
code to get this test to pass so we did um in our code we did uh empty list but actually what we want to do instead um
so you're looking at our test we need to be in the code yeah I know I was around the same time you said that I was going
wrong so code that we literally just changed we need to to modify so it's not that uh assignment uh and you could
probably combine that back with um with the actual assignment no NOP uh what you want to do is move the line down using
line down movement and then uh the combined lines J um and what we want is we want an else here so for column three we
were okay for temporarily right we're trying to do the minimal amount to to make it backwards compatible uh but here we
result but by doing that we broke line 75 by the way by pulling themes in no oh not when we finish writing this this
line of code okay sounds good right because we're going to do a return here so it's not going to hit line 77 but how
does this oh because it's out of scope oh we can fix that yeah yeah that was the thing we just moved into yeah sorry
you're right um because what we can do is uh we'll pull line 77 and 78 into 73 and a half Ah that's where you're heading
okay yeah got it we can do that now if you want because we're about to do a return in the Els anyway yeah got it okay so
you're saying result failure well we pretty much want to copy and paste what we've got above for uh the failure message
no not sorry above in in the current change right we basically want to copy and paste that result failure ah all of yeah
um minimum columns is going to be the wrong number because we're saying it has five is it five well five is is the only
number that's minimally greater than four so yes um because we're saying if we're going to process themes we need at
least five columns this stuff is temporary it's going to change as we as we move towards arbitrary columns um but for
now we we just needed to to do that symbolic okay here I mean hardcoded value uh we're going to change it anyway soon
right yeah if you want to do it that way I mean you could just put that J yeah uh and we can change our expectation uh
on the test above where it says must have at least four to must have at least five because I think that's what what
compatible and now we can actually start work so this is sending in the required columns but there's only three and the
columns right we want Contin yeah but we want to move toward it being based on the header and back to the required of
just uh three being correct artist song title and at yeah so this probably a a good place to commit since we're back to
to the green that we want are we totally green or no because the test the test right there is failing failing but that's
the only tal failing test that's our that's our our new Behavior test how should we phrase this want I'm joking um well
we changed our requirement right if we look at the the parser we've changed our minimum required columns to three that
was the main thing we did right yeah so that's the that's that was the main thing we did is is support um three because
that's what we want right we we we've been trying basically for the you know since since last stream is is to get it so
that really the minimum number of columns require is three but every time we tried to adjust it to four uh to to three
we run into problems and so we basically said okay well now we'll just have a default release type but now we're missing
themes um well actually that's if there if there aren't enough columns then uh the themes won't parse and actually that'
s okay uh so now we're shape so now now we finally get to to to do it a change of um passing in the headers because now
we want to map uh now we want to do mapping of header header uh the header columns to the actual content so we're gonna
you look thoughtful what do you think oh yeah I'm just trying to think of how we we would in a header to par song so it
knows what each column that's that's where it might start it might not be the right way to go but it's certainly a a
step in the right direction you said it might not be the right way to go do you have another thought well it may be
inconvenient to pass in the header row we might want somebody to pass in something nicer um row that's we've got a
failing test we don't need to write it out test we'd like to get this test to pass this test is is is not quite complete
um because it's not prepared to take the header so that that'll be the first step we take is that we pass in the header
that we have there commented out um and once we do that then we've got then the par song has everything it needs uh it
just doesn't use it yet something like this yep now if we do that that's going to change all the colors we do change
signature so they get called pass in blank for now well if we do that um well so let's see how many callers are there to
par song because we only have this test and the test above it I don't know that we have all that many calls yeah two
test and one production call right and the production call will adjust manually um to basically not do us uh to
basically grab the first line and hand that in but for now we'll we'll just pass in an empty string so yeah so let's go
ahead and change the the signature so let me undo this oh you don't need to undo that really it would change it if I do
all if we do that yep uh we want to add uh yeah that one it's funny is they're both strings and so it's saying which one
is the new parameter because it doesn't know although it kind of should um but it's the second one and that's why the
preview is so useful is because it says oh you're adding in a new parameter that's the first one that should be called
header yeah the preview is pretty sweet so so we want to provide a good default there so click into that ah there we go
I'm like where's the how do you get into it uh and I think the default values is going to be empty string we do that or
we it we to do um is that sufficient that's a string yeah okay I wasn't sure if I needed to do new string empty or
something like that String's a string okay all I mean so so this is an interesting thought I had um that I thought about
that I've used before when I'm explaining refactorings that refactoring is is the fanciest search and replace so we're
basically replacing all calls to par song takes a single parameter with all calls to par song Whatever you type in here
a comma and then what already is there so it's doing a search and replace of of those calls with whatever you type in
here so whatever you type in here is going to be what gets in the code and so how do you define an empty string two two
double quotes and so there's nothing special or fancy about it other than it has to be of the type of string right kind
it swegi continue or show conflicts uh no we're we're gonna um so we have a bunch of places where it's called Uh there's
three and that's interesting so intellig didn't tell us about those Lambda calls uh let's hit cancel I want to double
check uh and let's cancel out of this let's go to wrong it's actually missing all of the all the the method handle
versions of of par song there's more than one um oh maybe there is just the one yeah I thought it was just in here which
is pars all that's somehow I thought there were there were more but you're right that's the only one so what'll happen
is it's going to change that because it can no long because method handles only work if there's a single parameter right
um and so what it what intellig is going to do likely uh when we redo the the refactoring is it's going to change that
to be Lambda uh uh the Lambda form as opposed to the method handle form which is that's fine for some reason I thought
there was there was other usage that it wasn't picking up but that was in my head and not in reality uh all right so
let's redo the the refa let's actually refactoring yep nope wrong one yep I hate this dialogue because it's never as big
as I want it to be and so I'm constantly resizing this dialogue and this has been an issue with intellig for years and I
I knowing swing and awt layouts I know this is hard but they've got lots of smart people and they still haven't been
able to figure it out because usually it's like it's it's it's too small and I have to make it bigger both width and and
height um all right let refactor and yes we're fine with that and so we can see there on the bottom line 25 it did
exactly what what we expected it to um that will be an interesting change there all right so let's uh so now we're
passing in the header and so now there at least is is the possibility that uh that we could get this to work before we
passed into the header there was absolutely no way that this could work without it um yeah uh and in fact um I'm almost
wondering if we should should uh swap some of the columns so they're not even in the correct order uh but but we'll
maybe we'll write a separate test for that uh so now we'd like to use the header for for what what is actually what's
actually wrong how's this test failing again it's probably just doing it true false s with required column should have
so we test we could assert before it um the failure messages to see what they are well no we we we can we can we get to
to to to what we want so what's the difference between the way this method is calling parong and the way the parong and
I encourage you to look at song so what's the difference between the tests parameters and the production code parameters
production is getting a blank header test right right so what we can do is we can say if the header is blank we'll fall
back to things right because if we do that if so basically if you don't pass in a header we'll fall back and eventually
that fall back will go away but at least this again our goal is parallel change how do we support new functionality
without breaking existing functionality I mean cleaner than trying to do a different parse you know par song method to
right which takes a header and the other one doesn't and right the empty header is easier and cleaner yeah so let's do
that par song So we if a blank header we want to header you can just say is empty yeah is empty but do we want is if it'
s empty we want to just continue to do all that stuff or do we put all that in a giant if block well I mean what we
could do is uh before you even write the F statement extract the entire contents to another method yeah that's what I
was wondering yeah all of it the other method I guess we do we could say we can call this par header right and and in a
sense you know what you mentioned before about creating two methods one with a header parameter and one without that's
kind of what we're doing anyway um it's just a different sort of starting point to to get there and so now we can uh so
uh what you can do is um if you do surround with that's what I was trying to mentioned before is it a um oh no it's a
keybo Control Alt J Control Alt J but you have to be on the right your has to be in the right place yeah um sorry not
controlj that's surround width we want to actually Control Alt T oh that's the refact oh that's T oh so that's that
gives you the options of of an if and is if else um we probably want an if else and now you can just write empty and now
we can we know that the only thing that's calling it with a header is our test and so how do we get pass the simplest
thing that'll get it oh his success oh just really just return that's all the test is asking for right true and it's not
inspecting the song so it's it is expecting object but we can return null which really it shouldn't allow us to do uh
and actually doesn't know which um uh but we do want result success it's just that there's uh one that takes an
individual song one that takes a list of song um we can return an empty list that test wow yeah exactly it passed so now
so now it's clear that um our our test is is insufficiently precise uh but it was a step so now we want to ratchet up
our our expectations um yeah not that it returns success but also that it actually parses the song that here and here
again a dedicated result um assertion would be nice because then we could say assert song result is success and but we
do and I'm very tempted to to do that now but we're that would that would take us on a tangent so um well we need to
pull the the value out of now we can do yeah exactly in any order right well there's only one there's only one so order
and now we need to define the song that we expect that's see what the format yeah and you can hit um contrl P to see
what the order of parameters is yeah that I artist y wa a second no that's not the right be so the question is is what
do we want the release title and release type to be if right because we're saying that those aren't required columns
right what do want them to of Y what am I missing the red squiggle is unhappy oh next ch right prce there yeah and
that's where um uh control what is it don't tell me uh code completion control shift enter yes would have taken that so
I'm going to undo that here no over here control shift enter and that completes it yep sweet that's the top of my list
of shortcuts to work on yeah that's that's that's one of the ones I don't even think about anymore uh vegan is yeah I
agree I I I I think the way the status bar is is laid out is but honestly I don't I don't look at the status bar very
much because once the tests have run i' I've gotten the information I generally just don't even look at the status part
anymore all right run it well now it's gonna the code well now we've we've Ratched up our expectations now we need to
predict how it's gonna fail right well it's gonna we already know this is going to pass it'll be true right and it's
gonna come back with an empty collection yep instead of this yep so we expect it not to be empty and contain that but it
will be empty and does not contain it yep so fails as expected pass oh for the simplest way possible I think we I I
think it is worth it to do the the uh to to lie yeah I think you're going to want to use the the control W way of
copying because I think your prints are not going to be correct yeah I think they were wrong too I was gonna I was gonna
count on control Shi enter I did notice it I was probably getting them wrong success now that needs to be a collection
right let's see control P yep so we need to do well technically it takes a single right so theoretically this should
pass something yep okay great now I presume no nice try well we're done if that's the only song we ever want to bulk
import right with a header row right um so I presume we would ratchet this up more with a second so I think the way we
would yeah I think um or would we start dealing with the header before we go to second row I I think we would we would
write another test that has uh headers in a different order so basically the same the same song the same title the same
theme but in a different order um and that's going to be not going to work uh and and that will will guide us to finally
actually parsing uh the header row right this yeah and then changing just the header or well no we should we should make
it thing just move it over by one or yeah swap I think that's fine you've basically done a rotate so fine that's the
same that's the same should have succeeded and that's still the same fail this should fail with uh whoa well of course
it passed because we hardcoded the return um and so we want it to fail uh so we need we need to now for it so so our
other option is is we can uh generalize the code a little bit to use the actual inputs from the song um or we can
actually start uh because makes me a little nervous that we don't have a failing tests to tell us when we've succeeded
by by can basically use the the data that actually comes in uh so parse parse the columns and then hardcode the columns
into into line 60 there at the bottom so that still should result in failing um I'm not grocking the if that's an a
navigator instruction I'm not grocking too high level for me okay so what we want to do is um we want to parse so so
grab so copy line 65 there bottom 6 oh 65 right right right got it and put it in 59 and a half yep uh and then for the
artist basically just say columns Subzero no no no no no right where it says Earth Wind and Fire replace that string oh
with the actual column Sub Zero gotcha uh and gratitude one will fail and then thank you is column sub two and that
should continue to have the first test that passes in the header should fail right yep and if you scroll down here you
should be able to see the little so it's got the right pieces they're just in the wrong order which is as we would have
liked it to fail and now fail yeah the first time we would have preferred it to do that yeah yeah all right so we've got
a failing test um now we can probably do something uh we could do a prepare um while red uh no basically disable the red
test go back to to green and then prepare so we could do that or we could just continue on try to make the the test uh
the test pass but I I kind of like the the prepare sure let's do it so this and we should not be all green I don't think
we need to comment here because it's short lived it's basically disabled until we've prepared but I think we know that
that's what we want all right uh so now what we want to do is we want to have a method that given the header columns
tells us which artist so we're going to do a little um uh is that what you're about to say no uh let's pull zero out
into a variable so line 62 so do uh introduce variable no just the zero oh just the Zero part ah yeah because the only
thing that changes based on the header is which column is which kind know where you're going now column right so we're
basically saying create a new song with the artist column right columns using the artist column index uh and now what
we'd like to do is we'd like to change that hardcode of zero into something that's calculated based on the header right
so we want to find out is which column actually has the artist so let's write that wishful thinking method a separate
method okay so something like method that's fine fine fine all right let's run it that should that's that's totally uh
we'd like to actually not hardcode it um so let's parse our our header in the same way that we parsed the song itself
right there might be an easier way to do no so it's an array of columns they names is there a stream way to just say
which of these contains the word AR uh I think we we don't have to go to uh stream we can use the there's an arrays
class that might be good so let's see what methods it's got so we could convert to stream but we want to see if there
are other methods we don't need to do a binary search c wait a second equals no equals would be for the whole uh somehow
I thought that there would be a way to do that but maybe not uh so we can just convert it to a list okay is there a
convert to list yeah there's an arrays dot to list sorry of yeah eventually we'll probably do exactly something uh
something like that although I don't know that um we need to uh oh no yeah string string to in map yes that's what we'll
eventually do yes uh so what do what are we searching for what column are we searching for oh artist so just return that
actually we just yeah you could just say do return at the that yep cool so this is a backwards compatible change it
should it should still continue to work assum we assuming we did our our code here so this is what's nice about prepare
factoring if somehow we didn't use the index of correctly or maybe it returned a different value you know maybe it was
one based instead of zerob based um this will let us know because we were passing before returning a hard Code Zero we
expect this to still return zero uh we expect expect everything to still work so let's run our tests and if doesn't work
we know that there's something wrong with the code that we've written in that uh which column has artist but nope that
works fine cool and so now we would like to generalize this a bit um right because we want to replace column sub one
with another header based value something like this yeah and so I might actually do a introduce parameter on line 70 to
to get that out sense and this would be something like column right Callum now we really need better name I okay or col
or column index of either way yeah column index of header comma column name how does it look on the calling side looks
good should we reverse artist and header on the signature is it read no I would find that confusing index of right you
want the index of the header yeah passing it you you were gonna say something I think I yeah I was gonna say uh let's
now do that for the next column actually we could run the test right now and ti so the next one would be song title yeah
so what what I would what I would have done is is extracted the one assignment y okay run again should all pass because
they've got the one where we swapped The Columns disabled right and right now this is built for just one theme but I was
thinking using the word one o NE e oh CU it kind of reads weird or is it just me fine that that's a that's a preference
thing I I don't have a strong preference yeah I just felt like it was hard to parse the one versus an L right next to
the chair H and we are calling it uppercase theme one y rerun the test should everything should pass oh oh interesting
so uh we got a negative one uh or our Max is 10 so that's not the problem was it always 10 I thought we ratcheted that
down no no this is the max columns to parse not the minimum number of columns required this is the one that tells the
splitter how how how many how many times should I split before I return basically the rest of the string right um so
clearly it's the r code we just wrote which means uh we need to look at the tests to see because this is called return
success we interesting so we're getting the test we just wrote yeah so um oh you know what that header has a has a
backslash and in it and it shouldn't hypothesis yeah that was it good catch and so another reason why prepare
refactoring is valuable is because it might have been hard for us to to see that that was the problem when we were
trying to make the new test pass as opposed to doing the backwards compatible uh change here all right now if we
undisable this test uh it should just pass that's what yeah oh uh for for the same reason but now we know exactly why
because I copied and paste it yes but so much easier than if we we had enabled it and we were trying to get it to pass
and we're wondering why the the last value wasn't working right yeah I mean we solved that in a matter of 30 seconds
fful no welcome so now we uh now we have at least for this minimal case um we are headers uh minimal case meaning one
theme meaning one theme song title an artist and no other columns right but now we support at least those three columns
in any order right and um yeah never mind when we get to that the point where we start passing in album title then we'll
have to change yeah we have it has to be blank exactly yes yes um and we're already even before that we're at least with
my uh very primitive Obsession although I don't know if it's even primitive Obsession it's very much um column index of
header column index of header column index of header right so we've got three calls to the same method that takes the
same parameter there's something about header that feels like that code about which column is this found in um should
perhaps be a like a header object is what you're saying perhaps or a header index object because it's really about the
the index um or a header mapper that may be given that something Maps it for us so the entire mapping uh something like
that but there's there's clearly uh a fair amount of duplication and the duplication is basically a missing abstraction
of something that does does that job yeah um probably a good time for a break did you want to go to 12:30 I I could do
that I'm okay then let's take a short break uh and and we'll pick it up with expanding our tests to support uh basically
our our we want to get rid of par song without header that's our that's our goal we want all par song to be to be with
the header um so we'll take a short break and we'll come back and do that great right e uh so let's see uh where did
that go there it is tra of 52 so thank you for uh the compliment um escaping tutorial held by building projects
excellent um but doing a bunch of Googling doing a bunch of Googling is is is fine if you're doing a project um um the
main trick uh or difficulty is how do you break things down small enough so that you can finally so so you can sort of
take steps that get you in in a direction of stuff working um so the the question is is is do you feel like you're you
know so doing a bunch of Googling especially if you're learning new things that's that's what I do if you watch you know
here the stuff we're doing uh there's not a lot of Goog going on but if you watch my solo streams uh especially when I'm
working on my ensembl project I'm I'm doing a fair amount of you know searching around and trying to figure stuff out um
I don't have to do as much as as likely someone you know with with your experience because I've been doing this for 30
years so there's already a lot of stuff into my head um but certainly for new things like when I was doing my HDMX solo
streams uh I'm almost constantly searching because I don't know HDMX very well and so if you don't know something that's
what else you going to do you you search and that's totally fine uh let me just go on to to this so um you know you
shouldn't feel bad about searching for things that that you don't know how to do uh the question is is when you do
search and you find something do then make progress um because if you are uh then then that's fine so you're going to
basically do some stuff and you're going to say how do I do this like the the how do we figure out how we got an array
how do we find an element in that array we could have written a for Loop but feels like there should should be a better
way to do that and turns out converting it to a list and then doing that but I had to do a little bit of Googling to
figure that out because I don't do array stuff very much and so it's not in my head um we just didn't see the the
Googling because I was doing it on my screen and not not on Mike screen uh but then once we had that answer we could
make make progress and um the what I feel like is is difficult for a lot of people especially earlier in in their career
and novices is breaking things down small enough and knowing when the code you've written works right so this is where
um I encourage I encourage tdd or at least writing tests uh even if you don't do it first doing it frequently after you
write a bit of code because otherwise what what I see happen I do a lot of training and coaching uh both of individual
developers and and of teams is you're writing more and more stuff and you're still not sure if it works until you've
written a 100 lines 200 lines 300 lines of code and then you try it out and it doesn't work and now you've got 300 lines
of code to troubleshoot that's much much much much much harder than three lines of code like we just saw it's much
easier to troubleshoot three lines of code than 300 lines of code um but the way we've been taught and the way most
people are trained and the way we see other people do things as we tend to see you write right right right right and
then you maybe finally try something out uh and so breaking things down into smaller steps and what uh goo Hill calls um
many more much smaller steps and I add in a third s so it's 3M 3s is many more much smaller safer steps and that means
you have to break things down into something that can compile and run and hopefully you've got some tests written again
but if not you can at least figure out some way to works uh I I'll do I'll do a search for that um so G uh also known as
Michael hell but we know him as GW um think I've ever heard him called Michael Hill I always heard of this Mike Hill
Mike Michael um so uh by the way I this brings up the topic that I often discuss with usually individuals that I coach
um learning how to search is also a skill uh I watch my son do searches um and so he's on he's on the autism spectrum
and has got ADHD and I think that impacts some of his abilities and makes it more difficult for him but I see him do
searches that are pretty ineffective uh and I think effective searching using a good tool helps so I use kagi I think
it's pronounced kagi K AI um I don't use Google is my primary search mechanism because Google has has too much to be
honest crap um uh I pay for pay for kogi because it's worth it to me uh but learning how to search is a skill which
means when you search you have to you you I I think it's important if you're if you're not finding the things that you
want um take a step back and say what are you searching for are you searching in a way that's effective or he's
searching in a way that's that's not getting you what you want and if it's not getting you what you want what are you
searching for um so I could give you the link um luckily uh 3M and 2s is different enough uh and unique enough which is
why making uh searching for for that is easy versus searching for something like oh I want to learn how to do something
in go which was a terrible terrible language name now it's goang as one word is the way you search for it but that was a
terrible name from a ironically from a company that is a search engine uh so uh gpy hill.org is the site that has a
bunch of articles on many more much uh smaller steps so this there's not just one link there actually several ones um
but it's the idea is can I break this down into a smaller step and make progress that I can see visible progress may not
be visible to the end user that I'm creating the product for or whatever but it's can I see that I've gotten somewhere
um and that's really to me one of the most difficult Parts because it means you're breaking down large tasks into
smaller tasks into smaller tasks until you finally get down to something that oh this is two lines of code which is For
Better or For Worse a requirement to do tdd and that's why tdd I think is hard for folks certainly was difficult for me
um and I still struggle with this is how can we make smaller um how can we make progress but make that next step smaller
and getting better at that is is such a fundamental aspect of of being able to make progress more more uh more regularly
um and so I I saw um uh this mention um what I love about testrone development and I'm not saying everybody should do it
all the time um but I think pract doing some practice with it and getting a little bit of experience I think is worth it
because one of the thing it teaches you is that actually failures are good because it tells you that you're either going
in the right direction if it's an expected failure or you're going in the wrong direction because like what the heck
that shouldn't have failed um but because you're taking steps you know uh oh if it this didn't work you back up and you
say it must have been the code I wrote or as we just saw we had a a stray character that was causing the problem but it
it it tremendously Narrows down your your focus to what can go wrong right I just wrote one line of it was working
before now it's not that must mean that it was that one line of code so you back up but you're not backing up like a
day's worth of work or hours worth of work you're backing up five minutes 10 minutes maybe worth of work and then you
you can then you move forward again and I think these this idea of of small steps again even if you don't do tdd but you
have some way of knowing that that step I took was correct and I think tdd is a great way of figuring that out but it's
not necessarily the only way but it's the way I prefer um but it's that small step that is am I stepping in the right
direction or did I just step in the wrong direction and now working and one of the things that that TD does for me and
not just me I know it does it for a lot of people is um uh reduces anxiety because because you're taking small steps the
risks are low right you can he let me return a a blank string see what happens oh that didn't do what I expected let me
return something else well let me wrap it with an if statement uh but each thing is a small thing and if it fails we
didn't have much invested in the code we wrote it was again the small steps is not just is not just that you make
progress where you know if you have to abandon it it's it's not a big deal but it's also you you're not invested right
so there's the sunk cost fallacy and and loss aversion that we have as cognitive biases um it's much easier to throw
away two three lines of code than a 100 lines of code and oh sorry go I say the one thing that that also comes up is so
I'm my training is I'm a control systems engineer that was my college master's degree and so feedback loops are a big
part of control systems and so I map the world of control systems and feedback loops into this world and so in other
words like Ted said we just changed one line of code and it broke so our feedback is really tight in other words it's
you know within seconds or Mikey said minutes of when we made the change so we don't have as much to go over so your
feedback because it's tighter it's more accurate and it's faster versus a long feedback loop like I don't know you got a
really bad water heater and you turn on the hot you gota wait a while for it to get hot right that's a slow feedback
loop and then you find out you turned it up too high and the water's too hot and you burn yourself yep you got turn it
back down and it's like okay now I gotta wait half an hour to for it to to to adjust and like if you if you had to wait
half an hour to do an adjustment imagine how long that's going to take you versus if it took 10 seconds yep yeah the
feedback loops um and by its nature if you're taking small smaller steps your feedback loops are going to be more
frequent um I mean it's it's it's a mathematical formula the more you can do in in a certain amount of time and get
feedback on each step the the faster your feedback loops must be and and therefore you will be better so um Fofo asks
about uh so have code that's repeated uh and you may not have a clear idea of what's common and and so on and um I think
noticing the duplication noticing that code is has stuff in common it may not be pure duplication it may be just
similarity uh and I think noticing that is is is actually a good first step so noticing that's there making a note of it
uh and saying you know is there something going on here you may not know though right away what to do about it uh it may
not be clear enough you may not have enough examples uh you may not have enough similar usages um but at least saying
there's something here and then you can kind of be on the watch uh on the lookout for it um and then at some point
you're going to have to say okay there's there's an usually there's some kind of missing abstraction um what might that
be and so we saw um Mike I want to switch back to your clear uh so we can see here at the bottom line 62 through 64
right there's a lot of similarity right there's not pure duplication um if you look at full lines of code but if you
look at sort of subsections of that column index of is the method that's in common but in addition header is always the
first parameter so this leads me to believe that there's a missing abstraction around header now a lot of times people
will just say h that's fine right but if when I see common parameters passed in almost always the same thing uh or
parameters that travel together those are codes smells um those are things that may not be something you necessarily
want to fix right away but they are things that are saying there's something going on here that maybe we want to do
something about it's funny on that one I I saw the duplication as well but I didn't think abstraction and this is
probably my old C++ way of looking at things is like oh well that just means headers should maybe should be a field to
the CL class and you pass it in the Constructor and then you're done right why do we have to keep passing it in over and
over and over um but it was like we both noticed the similarity but had different thoughts about where to go you know
actually I like your approach better frankly um yeah I I tend to think like um because I'm always my my goal is always I
want to create more smaller objects so in addition to many more much smaller steps I want to create many more much
smaller objects um because what I tend to see is objects that have lots and lots of state so we could make header state
in the song parser uh but I feel like well then we're still calling a method that we're we have and if we make header
State well that's a string and so that then leads me down the road of primitive Obsession I'm like no this should be a
separate class right because what I because I always imagine like what if there was a header thing that could just say
what column are you um and that would bu by definition say oh there must be a header class and it has one method saying
which column is this in uh which what's the index of of this string uh and then it gives it to me um and then however
that's implemented whether it's doing a search through a list or whether as astd suggested before we create a map that's
then completely up to the implementation of of that class and it's not mixed up in all this this other stuff so many
more much smaller objects is is my phrase for to day speaking of uh uh your search for MMS so I did the same thing on
Google uhhuh Now if you look at this compared to what you got on kogi if you want to show your screening if you still
have it yeah um notice I just got two hits to Goot and for yours yeah this nice andly nested yeah and so that's one of
the nice things it does is is basically saying oh there's some on on the same site there's a bunch of related things so
there's first sketch there's a shortest distance FL optimization there's this other one um then we do get the podcast
like you saw on Google but then oh look there is uh this one which is probably the same one um I mean see that initial
grouping made me go I want to try kogi now yeah and what you can also what you can also do is is um I can say in any
time I do a search I'd like to raise anything that Goa has to say I want to raise its priority in my search and so I can
say raise and so it will then be ranked higher in any search I do um and I might say something else like I don't know
certainly want to basically in fact heck I certainly want to lower that I might even want to block it because it Ian not
care about that method yeah anyway so so so it has a lot of things it has a lot of features um so I I is that a pay one
you have to buy yeah uh I think there there's a free level but but I pay for it because um it has a bunch of other
features as well so out um yeah funny that when you're making money off of how things are displayed versus another
mechanism funny how that affects how things go uh so one other thing traa asked about was can I Implement tdd with
Spring Security yes uh it's a little bit more difficult because now you're dealing with one of the most complex modules
of spring which is Spring Security I bang my head against this the wall every time I I I work with it but you certainly
can and what's important there then is separation of concerns you want to test hey can I access this thing and basically
you're testing did you configure the framework correctly um and then at a different level you want to test does this
work with this kind of user where I'm not where it's no longer testing the framework now I'm just testing given this
role can can this person do that uh so that separation of concerns is um is another aspect uh sort of combined with
smaller steps that uh um and then one other thing was uh so was saying um in the design phase I don't tend to to sit
very long in the design phase so I I want to see code and I want to refactor from code because design you may sketch
things out and I'm not saying don't do any design certainly you want to do some design um but I and and and the folks I
I hang out with who uh uh tend to defer any deep understanding and because it it's it's fine to come up with some some
abstractions but I I mostly look at refactoring to create my new classes so for example could I have designed this
upfront to say we need some kind of header object that's going to know how to parse it probably um would it have been
designed exactly the way we needed maybe uh but because I'm really good at refactoring I don't I I can rely Less on sort
of bigger designs up front um but I do think some design up front is important but I wouldn't be worrying too much uh uh
about that especially for for things sorry about your knuckles crap trappa no fun yeah my my head h it's every time I I
do something slightly different with Spring Security uh it's I I basically it's one of those things where I don't have a
good mental model exactly for what's going on uh because it's very very very complex and it feels like a some of that
complexity if not maybe a large part but certainly some is is not essential complexity is is uh act I don't know even
accidental is the right word but it complicated yeah we'll never know less about what we need than than right now yeah
yeah we'll always know more in the future and so so I do sort of just enough design um but then I rely on being aware of
issues like this one duplication uh of fewest possible elements basically C you know kex you know four simple rules of
design um you know does it work uh does it is is everything clear you know fewest elements that kind of thing is really
for and oh two client been there oh man um if you if you're like within the guard rails of of like what the
documentation says here's here's how to do this or some of the tutorials by the minute you go off the reservation of it
uh it's uh yeah I mean you know again if if you're working with others you know and you're s and you're sitting around
whether it's a virtual whiteboard or a real one um and this goes back to the to the the the smaller steps you may want
to think about architecture actually how does the whole whole thing going to going to look but ultimately you're going
to be implementing a story of some sort something that's providing value to somebody um and you want to break that down
into small steps and so it's like okay what do we need to do here and if it's really small then then you can do a little
bit of design that takes you know coding so yeah so very much evolutionary design yeah evolutionary or Emer design do
and the the reason why that that um works for me uh is because I've made a lot of mistakes in the past uh in how I
design things and so you learn from that uh design patterns can sort of help although I don't think they're sufficient
certainly the way they're usually written about or taught about um but you sort of start gaining some some you know and
this is where good deliberate practice and kotas can can really help to to practice that kind of thing um but once you
actually Implement something you know you may have planned oh here's what the things we might need but then you
implement and you find oh these don't fit well together good thing I didn't write all that code up front uh yeah
optionality do I do this now do I do this later can I I always I always think about like can I procrastinate on this is
this effective procrastination or is this uh gonna gonna hurt me um if I can defer it because I'll know more and maybe
perhap and maybe come up with something better um then I might say I'm going to defer this because I don't quite
understand yet what the the abstraction is uh and there are a bunch optionality all right so um do we want since we've
been te talking about abstractions do we want to abstract out header of course after we do a a commit which we should
have done let's do the commit first yeah all right uh we basically support um header columns assuming minimally required
means just one thing why yes we require we require at least yeah okay you want to do that um deal with the Primitive
Obsession now since we talked about it and probably I think so I think so at least we'll get it started um yeah probably
won't won't won't finish it but started um and we're green just double check yeah you know we haven't run is all in a
while ah yes uh hopefully that's okay yeah but let's find out oh they actually have been haven't the all been running or
oh during the commits they are did it run all or or the io free let's run well sure yeah I forget what the commit I'm
pretty sure the commits run all or is it only on push it's been a while I forget uh no it's on Commit th commit okay so
they passed okay cool sweet empty um that one is the wiring of parse to of parsol to pars song passing in the header
maybe we want to make that work that should be really straightforward so let's let's uh enable it so it should fail
because we're not handing the header we're just handing an empty string so that should fail yeah um but parsol we haven'
t dealt with right so now it should be it should be that so we'll need to go into parsall and extract the in do we pass
in header to no we we got it we parse the first line right so what we want to do is extract the the tsv song lines skip
one uh and pull out and and assign the header from that so for this and then do a a local ve or so yes extract variable
yeah extract variable that's what I meant to say yeah yeah what we call this um this would be our song stream skip is
sort of Skip and let's uh remove the skip because we no longer want to skip we actually want to grab that yeah so we
don't want any dot there Y no dot at all okay but before we do the filter we want to um get the first element uh no no
so you want to just move the semicolon up because that's it line then what we want to do is we want to uh from song
stream we want to get is it called get next line uh I don't uh uh it's so rare that you basically just um what would it
be because it's it's basically is it a peak I mean I guess we one uh it's got of I mean we could just since we're handed
uh a list we could just grab it from the list and still do the skip um oh we're not hand a list we're a string that we
then parse with lines uh it's too few lines to that make sure there's at least L does I guess we could just do a fine
first uh it'll return an optional but we know there's going to be that one because we've already ensured that on line
get like that or yeah so UND undo a few times because you want to get back to without the variable definition yeah let's
do a a get um uh actually I think we want to just else um here or else no no so instead of the get or else get or or
else um what we want is or else and then an empty string so basically it will return the first element but if it's not
there for some reason we'll get an empty string and now we want to sign an optional right and that's our and that's our
header y yep then we replace this with yep H yep now everything should continue to work and I'm curious what intellig is
highlighting there on song stream uh oh because fine first is a terminal operation oh we broke the stream Peak because
uh fine first is a is a terminal operator um so yeah so we're going to have to use Peak so instead of fine peak um we
don't actually want to do anything oh Pik is just gonna so action is what the peak is going to do uh and there's no good
way all right we'll have to convert the stream to a list and then uh and then turn it back into a stream that's this
there might be this um yeah uh yeah there's no point in holding on to song stream so you can just inline list uh and
then inline song stream one and then uh delete that line yeah and then song and then you got to do do stream to convert
it to a stream now we're back uh let's create the header variable we've right uh the header variable we get from so if
you click on header that's currently red we can go ahead and have it create the variable I just have a cre cut it does
it not want to create the variable for us all right we'll have to do it manually that's weird why not sure what it
thinks it is okay uh let's assign that to a blank string because that's what it was before so this should be equivalent
to what we right uh delete that somehow that got that's what got imported by header and that's why that's why we header
recogn that's why header looked weird uh okay we broke something um probably because we we took out the skip so let's
put the skip back in all right One okay right so that's the that's the one we were trying to make pass right um so now
what we can do is assign header to stream list first there we go that should do it right let's see nope uh did we not
enforce passing at a time let's see let's see would in parse so we said two few lines in uh okay so we required it uh to
have two lines okay so it's something else um oh okay well so basically we're not yet ready to do what what we want to
do oh don't fully par yeah we don't fully parse if we're given a header we switch modes and we only know how to parse
three things when we're given a header so we can't do this just yet so let's red Dis Let's uh undo the change uh let's
um Undo It by doing this part yeah that's all we want to go back to yeah yeah and then we want to disable the test above
saying um we can only do this parsed y now we should go with two disabled in y yeah as we could use the peak and and get
a holder object and it's not worth it um there might be some other way to to do that but there it's really awkward
because we'd have to do a peak and then in that Lambda we'd assign it to something that could hold a value because you
can't do it uh and then it supplier this is easier uh this is probably a good point to stop Dar we do the header thing
but yeah yeah so uh let's check jira um so I think we've done it at least for the three those three columns uh we have
not done it for the yeah so we want to support uh columns other basically and just remove the ones we already here uh
and we might want to call out that that we want theme two three and four um that we already handle theme one so
basically support something maybe say something after to support these remaining columns that we say uh we do three work
on three theme two three and four first uh is that what you meant no it's just call out that we've already done theme
one but we haven't I was going to put that on on the line above it because we may not notice it if yeah hey I guess we
can always write our own collector uh it would be an interesting exercise and that would definitely be something I'd be
doing a lot of for well not just the PMS but we will be happy next time um and I think it's actually kind of funny when
when we started the stream we actually didn't look at CH we kind of knew where we were we do right or at least we
thought we knew where we were um so the other thing we might want to note even though it'll probably pop up again but we
may as well refactoring even though you should never put refactoring items in Jura we're doing it um well we could say
it as a yeah yeah and what is that uh parol or is it no it's parong I yeah h i shouldn't be yeah yeah yeah I wanted to I
wanted to grab this I don't know how that's fine I think we'll get itol all right so um that's all for today folks uh so
we will be streaming again tomorrow um we'll be starting half an hour earlier than we did today uh although for those of
you who didn't keep up with the time change uh it'll be half an hour later or something um but anyway it'll be 9:00 am
Pacific time which is 4M UTC so it used to be 5m UTC now it's 4M UTC uh and it will be um so we're basically minus 7
from from UTC and that won't change until October uh I think October but for those of you in in Europe you're probably
going to adjust your time zone relative changes uh in in a few weeks um but regardless our our 4pm UTC will not change
you will just have to figure out what that is in your time zone I'm looking at the chat about story points and it's a
good thing we're ending because I would go on a rant and well yep if you're if you're whatever relative to UT so you're
UTC plus1 um and that might or might not change for you at the end of March depending on where you are so um so that's
it thanks thanks for hanging out thanks for all the the great questions and chatting and so on uh and we'll see you uh
we'll see you tomorrow everyone
