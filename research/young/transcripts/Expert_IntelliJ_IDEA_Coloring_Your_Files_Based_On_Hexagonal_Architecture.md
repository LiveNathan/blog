# Expert IntelliJ IDEA： Coloring Your Files Based On Hexagonal Architecture

**Video URL:** https://www.youtube.com/watch?v=pavYN7Yy2pQ

---

## Transcript

hey there this is tedem young also known as jitter ted and so today's video is about coloring your files so normally we
don't think much about the colors of the files as they appear in our project window we may notice when files have
changed so they go from sort of depending on your color scheme black on white maybe blue uh or green so typically if
you're using git it'll show as blue if it's changed but it's already in get or green if it's new to get uh sometimes it'
ll show as red as uh being new and not added to get so there's some coloring of the file names themselves but that's not
what i'm going to talk about here what i'm going to talk about here are the colors that you might see here we see that
not only do we have background coloring in our editor tabs but we also have background coloring in the project window
and so what i've done here is i've colored the different packages according to their place in the hexagonal architecture
so some of the background color you may be used to because intellij idea colors the test files in this sort of light
green hopefully enticing you to make your test pass however normally there's no other coloring for your production code
files so what i want to show here is how you can change the coloring and make different background colors depending on
the part of the hexagonal architecture that they're in so for example here i've got this yellow which is the color that
i tend to use when i'm coloring the domain in hexagonal architecture diagrams i've got this sort of orange peach-ish
color for the applications or the wrapper layer around the domain that's still inside the hexagon and then i've got
colors for the adapters and i color the inbound or driving adapters differently from my outbound or driven adapters so
we've got this light blue for the inbound adapters and then the sort of purple lavender color for outbound adapters and
that's sort where the color scheme that i've used but of course you can do whatever you want so let's take a look at
where we want to go so we can get to the properties that control the coloring it's really two pieces one is what are
called scopes so i don't know about you but i don't know very many people who use sort of custom scopes but it's there
and one of the advantages of this idea of scopes is the coloring there are other advantages but that's that's what we're
going to use it for here so we'll see if you press the click on the gear in the project window you'll see edit scopes
and so we can see here we've got four different scopes then what we can do is once we have the scopes defined we assign
file colors to them and so we can say whether we want to enable those colors do we want to see them in the editor tabs
maybe that's too annoying certainly i want to see them in the project view so we can turn those off and off the other
thing is normally you probably want to share these unless maybe your team doesn't like the colors but you can share
these through the vcs through git and it'll basically create a separate file that you can then share in the repository
otherwise it keeps it locally and then it's not shared so once you have each of the scopes defined you can then assign
colors to them now one thing you'll see is that we defined four scopes domain incoming adapters outgoing adapters and
application file callers though has six different entries because there are default scopes in fact if you do nothing you
will see that there's basically tests and non-project files and then basically every nothing else so let's go look at my
mob registration system also known as ensembler and add color coding for that so here we can see our production code is
all in white it's still all separated and organized according to hexagonal architecture but there's no coloring we see
that our test code is in is in green and it happens to automatically color sort of target files and other files in
yellow but i'm fine with reusing that since i won't normally see that so we'll go first and edit scopes we'll see there
are none we can take a quick look at file colors and see here the two default scopes with their two default coloring so
tests are green and if you don't like it maybe you want them red totally your choice you can do that and then basically
non-project files like this target and other things will be colored yellow but we want to add some new scopes so click
here on the plus and we can say either local these won't be committed to the repository or shared i'm going to make them
shared and i'm going to add this scope and this is going to be domain so we'll start sort of from the inside out so now
we got the name assigned and now we have to say what is part of this scope there's a bunch of different things you can
do the easiest is i'm going to say in my production classes i want anything that is domain to be included and i want
recursive right so i want all packages underneath that so we'll say include recursively and it basically uses this
pattern of src for the source directory the package name uh and then it uses this dot dot star to basically say include
recursively if i just wanted the package and just include it without being recursed then i'd have just dot star and note
that since i clicked both it actually included both because it combined these with an or so you don't have to just pick
one directory and that directory and all of its subdirectories you can actually pick a variety of different things so
maybe you want to color domain and application the same so you can select domain and then click on application and say i
want to include that recursively and include both of them but i don't want to do that i want my application differently
so we'll stick with just domain so we'll go in our production classes we'll find application we'll say include
recursively then we'll do our so that's in production classes under adapter and that's basically out now since it
compressed all the things uh we can basically say let's not compact those middle packages because we actually need to
grab the middle package so here what we want is we want adapter what we want the outbound adapter and then we'll pick
adapter out we'll say include recursively but we know that we don't need the jdbc so we'll just delete that and one of
the things you'll already notice is that it's selected in green the ones that we're currently working with so that way
we we know it worked it's and it also tells us the scope contains 23 out of some number of thousands of files so that
was the outbound and now we'll so here the same thing we want adapter in but we want all adapter ends so we'll go ahead
and include recursively and then remove web and now we see all three of these are included so that basically defined our
scope so now if we go to file colors we'll see that we can now add these additional scopes so we're going to say domain
is going to be yellow and then we're going to say application and then we want our inbound adapter to be sort of blue
and our outbound adapter i guess they call it violet and we want to share the file color information as well through vcs
so we'll and once you click ok you'll notice that the files are now colored according to where they are in the scopes
which we've based them on where they are in the hexagonal architecture so that's it for file coloring and scopes hope
that was useful thank you very much
