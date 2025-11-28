# 14 Java Refactorings You Need to Know in IntelliJ IDEA

**Video URL:** https://www.youtube.com/watch?v=j9LRuU_SXZo

---

## Transcript

foreign it's less it's not really navigation it's more um selection so the magic key is uh at least on wind on Windows
it's control w but it's a completely different shortcut on the Mac unless you're using a different shortcut uh theme
setting configuration but the sort of the the the current up-to-date Mac uh shortcut set is basically option up Arrow
and so wherever your cursor is it's going to select the the thing that's that's that's basically around your cursor
whatever makes sense depending on the context so here if I do up Arrow it's going to select the word event and that will
depend on whether you have camel case selection up on or off um then when I do it again as you extend selection it
extends it in a smart way so now it's selected game event if I do it again it'll expand it to the whole selection if I
do it again it expands it to the method plus the parameter again now it's the basically entire statement the statement
includes including the Terminator a full line the contents of the method the contents of the method including the
curlies and then the entire method definition and you can keep going uh now basically nice and even out the block that
surrounds it um including the space and now the entire contents of the class but not including the curlies yet now the
entire console of the class including any white space now including the curlies now the entire definition of the class
uh and you keep going and now you have the entire definition of the file what's nice is if you reverse it so now you
want to narrow your selection because you realize you went too far um you just keep hitting the shrink selection and it
does it in the reverse order I use this all the time and I don't even notice when I use it anymore so if I start here it
will start selecting this way and select the method um if I start in here it's going to select the in inside of the
string the outside of the string now the entire parameter and so on and so forth um shrink selection goes in reverse
which is option down arrow or Ctrl shift w ow so this extends if you're using IntelliJ you should be using extend and
Shrink selection all the time you will you will if this works really well with uh refactorings for example if I want to
go and refactor in my game uh my game View let's say I want to refactor as I want to refactor this into a method so I
select it now I've selected it the expression um and it's smart because it no it's it's Java aware just like IntelliJ
Java where it's smart and so now I can extract this right so it works very well hand in hand with refactoring because
often you select more you know a certain block uh and then hit extract or rename or or um I don't know why it didn't say
cart here it's a string of card so in here owner now selected the whole thing uh so sometimes it selects too much when
you've got like string concatenation because it doesn't know what else you might want to select uh but if I'm here I can
select player player hand all the parameters the whole method uh or the entire string for the entire return thing and so
here I can right and I just do it quickly and it just does the right thing so expand and and uh shrink selection I use
um the next thing I use all the time uh is honestly all of the the refactoring stuff and so the keystrokes um are laid
out or designed in a way that that I think are make it easy to remember so for example if I want to um extract this into
a variable uh on the Mac it's command option um it's a command or Control Alt B on uh on Windows or Linux so command
option or Control Alt are always going to be the prefix the The Meta keys that you hold down or most of your extract
kind of refactorings so extract variable will be those two keystrokes plus V for a variable um M for method C for
constant but I can't figure out what a constant is here but I can pull right and those are the ones I generally use
right V for variable M for extract into method P for extracting it and pulling out a parameter C for extracting it to a
constant um if I ever need to go the other way around n is for inline all right so those five are the top five
refactorings that I'm doing almost all the time the ones that don't sort of live on those keystrokes uh that I use all
the time is rename which is um shift F6 use that all the time in fact I probably do renames I wonder which I do more so
uh let me go create a file so number one is uh extend extender expand so extend selection so basically extend string
selection and my number one keystroke uh and then two through six are the uh command option or Control Alt um
refactorings so that's uh V for variable uh M or method C for constant at a final P4 parameter argument um that's two
three four five I guess that's two through five but there's another one and rename is context sensitive uh this one is
uh option up down arrow w uh yes exabyte Vim has has similar stuff yes sorry I missed that uh so rename shift F6 is
context sensitive right so I can rename uh a method I can rename whoops I can rename this method I can rename this enum
I can rename this class right so it's context sensitive it'll do the right thing it is among the the most generally safe
refactoring automated refactorings um uh there's sensitive then there's a bunch of uh navigation stuff I am constantly
navigating so the two big navigation things I do are you just saw uh which is recent files I'm basically putting
together my top because somebody I forget now who asked and maybe they're not even here anymore but I've been meaning to
do this anyway is my my top 10 IntelliJ shortcuts so recent files command e stop so this is this is under the stop
scanning the list of open tabs and stop scanning your list of files to move from file to file either use recent files so
command e and I'm constantly doing that when I'm switching back and forth between two files so command e enter basically
flips me back to the previous one so this is the recent files which you um control e uh command o so basically search
for file uh that's command o or Ctrl n uh that took me a while to relearn because it was it's command o not command M
because command n is something else so basically these two are used um when I'm basically navigating files I do not I
see a lot of folks they'll have their you'll notice that I don't even have my editor tabs here on top a lot of times
I'll see people scan okay where is that Tab and if they don't have an alphabetical order you're basically doing a linear
search that's slow even if it is an alphabetical order and you're doing a binary sort of a mental binary search it's
still slow it is much faster to say I want to go to Blackjack servlet I will hit command o blackjack servlet um eve even
scanning the project window is slower than typing Commando and that's assuming you're not uh on the file itself so the
last one for navigation is jump to definition use and that's command B um so if I'm here in blackjack servlet and I want
to say okay game view where else is that used so here's I've um defined this but I can also revert it reverse it I can
say okay I'm on the definition of the Constructor uh where is it used and so now it pops up a window of where it's used
and I can go back to my test and I can say okay where is this defined so command b or control B and then where is this
used again command b or control B tells me where it's used I can jump there um shift shift is is is is is okay if you're
not sure what you're looking for um I don't like the double tap stuff um I know if I'm going to class I just do commando
which uses uh the fingers on both both hands which makes it a little bit faster um and I know it can search for a class
and not just everything if I am shirt searching for an action like I know I want to do something in IntelliJ but I don't
remember what it is um I just use command shift a uh so shift shift brings up the the general all search which searches
everything classes files symbols actions um occasionally I do um a search for oops uh that's in line occasionally I do a
search for a symbol but not very often so um yeah the problem with double shift is if it is for me is it searches
usually more than I wanted to search um but definitely valuable uh so that's kind of the top ten did I go on or should I
end the stream here because there's others but those those are the those are the big ones um there's probably a couple
of others that I use commonly that I'm not even aware of but one thing that I find really really useful is no editor
tabs stop scanning for Stuff use Commando or command e to move from file to file it is much faster um and you're
spending less time uh I whenever I'm teaching and I'm like watching my students work and even when I'm watching people
who've been working for a while I'm constantly see them going now where is that oh here it is where is that and here it
is right um and so uh spend less time just just type what you want to find you can use the camel case kind of stuff
right so if I want to go to um the Blackjack servlet I can just type BL s and it finds everything that starts with BL s
and that's Blackjack server uh this is the Blackjack game that we there is also double tap control which will run
anything um but I don't use that one I actually use uh command option R so when I want to run stuff so I'm going to make
that my bonus uh on Windows but on the Mac it's uh control option r the control option R gives me all my run
configurations um and I often have these here because my goal is I don't want to have to use my trackpad Mouse whatever
to find what the Run thing is and then right click on it and find the Run thing right I just want to run it uh and sort
of relation to that um I guess I'm going for for more than 10. uh is run current context and I do this all the time when
I'm in my tests so if I go to my tests let's say here unless I just wanted to run this test and I didn't want to run any
others right I want to run the test that this method that my cursor is in so if in I'm inside the method it will run
just that test method if I'm outside the test method but I'm inside a test class and I'd hit Ctrl shift r um then it
will run all the test methods in that class so those are really handy oh hydrate oh I didn't get my other
non-caffeinated drink I guess this will have to do I normally don't drink coffee this late but to run current context
especially useful in in tests but it works wherever you've got something that's runnable like your main method now I'm
thinking do I use anything else I'll use move and copy occasionally less often but I'll use those um uh there's
something here it is uh so this is interesting I don't look at it very often uh but it's interesting to look at so this
can tell you yeah if you're a mouse user you're gonna have different habits I am I am definitely an I I want my hands on
the keys um because I I for me I find that to be the the most productive way to work um having to for me to move my
fingers to the track pad um is a little bit extra extra work and requires a bit more precise precise movement but yeah
some people some folks yeah they live on on their Mouse oh control y uh control y would be command delete which would
delete a current line so the couple of up things there but so what's interesting is this tells you I use variable name
completion um most often syntax aware selection uh which is the the selection stuff I use that next most often and then
so basically my the auto completion stuff I don't even notice that I'm doing it um because I use it so often clearly
recent file pop-ups I use a lot uh go to declaration I use fairly often an editor delete line which is control y on
Windows or command delete to delete the whole line I guess I use more often than I thought oh complete statement oh my
God how could I forgotten a complete statement foreign statement when I learned this uh life was so much better this is
uh uh Pro shift and windows so complete statement is awesome let's say I am here typing this and I'm saying as HTML body
uh so I can select it and now it's like I need the semicolon so I can hit command shift enter which completes the
statement so even if I was doing this and it didn't close the parenthesis for me uh command shift enter will close any
open parentheses and Tack on a semicolon at and I'll post this um somewhere I'll post probably post this in my Discord
and then I'll sort of make a full full blog blog post about it complete statement use this all I once I learned this I
now use it all the time um so this closes open prints uh ads final semicolon uh I don't know what it is on Windows let's
go see oh let's take a look at your issues yeah um yeah so rename I talked about that's quick dock up top that F1 yeah
um these are pretty well known so I probably I don't actually use them that much because I don't um post-fix completion
that's a whole I like that quick fixes have saved you from 964 possible bugs uh show usages so what's interesting is I
is I used to use this keyboard combination a lot show usages except somewhere in the past six months IntelliJ said well
if you're on the places defined command B will show you its usages it used to be a separate keystroke but now it's
basically both are under control b or command B what I mean by that again is um here render hands where is it defined
command B takes me to it and I used to hit uh command option F7 to take me to where it was used but Now command B does
the same thing so I hit command B command B I can go to render welcome command B takes me to the definition and then
command B takes me to where it's used it's only used in one place render submit button takes me to the definition now
since there are multiple uses it'll pop up which one do you want um um speed searching trees we I mentioned that but
implementation I just said show usages is the flip of that uh introduce variable I use that all the um smart enter
multiple carrots I'm trying to teach myself to use this better there's still some stuff that I haven't figured out how
to smoothly use so uh variable and completion code completion syntax aware selection finish look up by special
characters uh refactoring down here yeah so it's really interesting that that it collects those statistics I think again
this is something I learned I don't know over the past year or two um and it's kind of cool because you can look at the
stuff that you don't use and maybe you should use more often um like there's stuff I don't use much at all I don't do
switcher at all because I'm using uh uh recent stuff code completion has saved me from typing 32k characters uh but
that's for me since 2019 but I also use two computers so it sort of spread across two computers I also don't know how
much it resets every um it must because clearly I've been upgrading since then um but you've clearly been writing more
um the other one I use a fair amount is F2 uh which jumps to the next error so I'll yeah I must save it in some Global
place on a computer I don't think it's like per account because I'd have to check my other computer because this
computer I actually don't use as much as as my other one because my other one's my travel one well actually over the
past six months this one I've used much more so uh so F2 is really handy because let's say I'm here um it'll take me to
anything that is suspicious or highlighted as either an error or a warning you know a bad variable uh F2 will take me
there so I can be all the way up here and F2 Bambi takes me the definition command B all right we've spent a lot of time
today over six hours uh and I think we're done so uh these are these probably are maybe not in strict order but these
are the ones that I use most frequently in terms of my shortcuts I'll probably add one more to make it top 15 because
top 14 sounds really weird
