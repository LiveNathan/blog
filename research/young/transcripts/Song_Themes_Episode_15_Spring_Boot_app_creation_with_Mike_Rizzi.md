# ＂Song Themes＂ Episode 15： Spring Boot app creation with Mike Rizzi

**Video URL:** https://www.youtube.com/watch?v=4rG7Im2DdKM

---

## Transcript

all right hello folks welcome to another pairing yay uh so today we're gonna try again uh to get some authorization
authentication working this time we'll use a hopefully time is there stuff we need to rip out I guess we'll find out uh
yeah we're gonna pretty much rip out we might even just version um one thing that that I just find interesting about the
market for authentication authorization stuff is most of it is aimed at like front end like single page applications or
or back ends that are not Java and it's really it's one of those things is like it makes me feel like I'm I'm no longer
with it like I'm using some outdated obsolete technology uh because if Java is mentioned it's sort of like an
afterthought um in in a lot of these um and then there's some where it's where it's not even Java's not even mentioned
at all and it's just like not like Java's dying it's just um and I've used uh other other tools um but like the ones
that seem to be aimed at like I don't you know we don't want to run our authorization server like actually you know
spring boot has has an oo resource server that you could run um and you could run keycloak which is basically an
authorization thing but like just like I don't want to you know set up AWS I don't want to run an authorization server
and and so on um so yeah it's it's a little bit little bit I don't know I don't know if frustrating is the right word
it's it's more um disheartening maybe a little bit yeah or you know and also the sense of sort of like feeling left out
so um but but kinda looks uh looks reasonable um oh hey astd yes sorry we're we're stepping on uh on agile lunch and
learn which reminds me by the way uh and I and I keep forgetting to to promote this cuz I don't know about you but like
when I look at my calendar I'm mainly looking at the week um and then so when uh stuff happens next week I I'm like oh
right there's stuff happening next week and so um so next week uh actually around during this time uh I'm doing uh a
thing on my tddd game with the agile lunch and learn so I'll I'll post a link to that uh later um and I'll I'll post
that I got to remind myself to post that in in my Discord as well so so that should be fun that's that that'll happen
next week uh but anyway so um so let's let's get to it uh let's go see where we are with your code I will now move
streamyard off are so I wonder if we have any even um some uncommitted yeah we definitely have uncommitted stuff um but
then before that it's interesting what was there yeah so what's what's uh why don't you do a diff on on the palom file
so if you click on pal and then just show di show diff or new tab uh show diff put in a new tab anyway um I don't know
about you but I like it to pop up as a window whenever I do side by side or top bottom um because it pops it in an
editor tab uh I find it annoying you can actually have it pop up as a as a new window on top if you go into settings and
then go into advanced bottom uh and then type diff in the search that and you know what I'm GNA do yeah so it's so it's
interesting it's like uh before I I started doing the side by side or the top bottom editor tab set up um having it pop
in the edit tab was was really nice uh but now because it pops it in an edit tab that takes up half the space um it's
actually really annoying uh so I'm glad they had that as a setting so let's see um that's we were figuring stuff I think
that uh only change no the orang the Orange is no no so so only uh stuff that's blue is is changed if you look in the
rightmost gutter on the side so that's the only thing that's changed is basically we commented out postgress uh which we
can leave commented out so that's fine that's just when we were trying to troubleshoot uh superpa base um our
application yamama we can file you could have done the delete from there too you can yep just right click delete oh
there it is or press the delete button that works too uh application properties um yeah it's not showing all the diffs
so we'll just we'll just set that back let's delete everything from line three to the end on the right there in
properties um and let's go back into the Palm file so we'll just go into the editor for the palom file so not the diff
yeah I know I know you could do it in diff but this I was wondering if it would if there was a if double click would do
a diff or whe it would open the file you could uh I assume double clicked that did the diff right it did yeah yeah
because that's what you that's what you kind of want so yeah I was just testing it that's why I did that okay uh so what
we want to do is we want to find the um uh the library we added for super base HTM X so just you can search for it you
can just scroll down there it is yep uh let's get rid of fault um we're on 322 right of uh of java of the sorry spring
boot just go to the top of the file yeah okay good all right um let's run all of our are and we could look also at the
commit history but I don't think we changed any anything important uh we may have added some end points but we can take
a look at that all right so all the tests are passing uh let's just do open up the the G gotcha so yeah so essentially
we haven't really done anything since we we haven't committed anything so right uh so we're and it all passed y sweet
all right um well let's do let's do a commit uh just basically you know say we to not yeah can you bring up the get tool
window again because I think we're were looking at the wrong thing yeah we don't want to look at the remote we want to
look at that because you had some a bunch of unpushed changes no uh you're not scrolled all ah yeah so if you click on
starting down off path click on that one uh so we did make some changes we did some renames that's fine uh that was just
a rename and we had changed the pom file to add the things that's fine okay y we're good okay yeah all right so um the
first thing we'll want to do is uh sign up for for Kinder h okay let me actually make sure my Vault yep is turned off on
the other computer let me bring it up here actually we hide my window for a sec yep right there we go let me see if I
already have kindall not the same no so let me bring can well actually it's I should just do the startup for free right
yes uh it is unlikely we will ever hit uh more than 10,500 monthly active users so um it's interesting they have a
contest uh for um doing a speedrun for setting up authentication uh which I think is kind of a interesting little
contest interesting that they do the uh please give us your first name and give yeah folks don't do that don't ask for
first and last name separately unless you are the government in which case you know what you're doing uh usually in
terms of filling out form although it was funny uh what was it uh there's something governmental and uh you you click on
to sign up and you basically get a Google form which I thought was like what really yikes kind of yeah that's kind of
yikes um but it was official US Government stuff so oh but but yeah don't don't ask for first name and last name if you'
re going to ask for first name and last name you get then you are required to ask for uh other names as well um and you
don't want to do that so don't do that just name forgot to mute um it's asking for kinda domain and if I type it has
actually you can actually share the screen for a okay oops there we go so it's showing business name so if I put in my
business name it's going to start oh it did before interesting it was starting to mirror let me just it was typing
whatever I typed here in before the in that place right that makes sense because it's basically guessing that that's
probably what you want as your subdomain ah okay I thought it was gonna force me down that path so we'll do song themes
right um yeah that's fine you're probably you're probably not what were you thinking well generally this domain would be
for all auth your all of your authentication needs um because this domain would be specific for your business uh for
your entity that might have multiple applications um right but you can leave it a song themes I you can or should I not
I'm pretty sure I really think it doesn't matter just call it you know you could just call it song R open source or
something cool this is and you know I know I rant like uh there's a really good group that does user uh user you know UI
and user research and one of the things they found uh especially for long forms this isn't a ter terribly long form but
one of the things they point out is it's really important to tell people why are you asking me for this information
right like why are you asking me for business name what are you going to use that for what does it actually mean um and
Kindle domain to what does that mean what what are you going to use that for how does that affect my application and I
and I find that that a lot of this kind of stuff gets short shrift and what I think companies especially startups like
this don't realize is you know they always talk about you know this idea of a funnel and people you know jump off the
funnel and don't end up trying things out for exactly this reason it's like I don't know what you're going to use this
for am I locking myself into this can I change it later um all these questions that you were asking that that I'm also
asking it's like don't just assume we're just going to throw and give you information without understanding what it's
used for and it's not necessarily even always like a privacy issue it's more like if I give to can I ever change it will
this affect me for for my entire life right and these are these are things that that cause people to move to something
else um and I think these kinds of things are don't take a lot of effort uh other than having to consider it and uh it's
it's it's unfortunate that that not very many like there is a couple places that do exactly that it's like here's what
we're going to use it for there's a little question mark that you can Mouse over and it'll tell you a little bit more
about it it there a link to some help um so I think uh you know these are these are important things and if you're
designing applications that ask for information you want to be really clear about why you're asking for that information
yeah um I think I'm not sure what's next so maybe we should or I'll just pick me off uh yeah let me since we don't know
yeah and this yeah this is kind of the the the funny is like what what sensitive now information are you going point ah
didn't like the hyphen the Kebab case in see like Why didn't it tell us that why didn't it tell you that why didn't it
have a little regex in the input field like folks the stuff isn't hard but you are hurting your business by doing this
stuff especially like this is not hard stuff this is just not hard you're just not thinking you're not having empathy
for your potential customer um says start a project from scratch or use kinda with an existing code base I imagine
existing codebase uh I guess so because it doesn't say whose codebase existing Kinder codebase you know what I mean
again it's the okay I'll do with existing let's see what Java should I show yeah you can show go yeah I mean this
doesn't matter because yeah so you can just oh this is them telling you what they have sdks for it's a yeah so it's
basically asking you so it can guide you to the specific docs part right um but unfortunately their um mainly because I
kind of like again this is where it's it's like clearly they don't understand the Java Market because you would not
provide a Java SDK without considering Frameworks like spring oh interesting like why would you do that in in 2024 why
would you provide support for Java without explicitly saying here's how to use it with spring that that to me is just
like you don't understand the market which again you know we we are the the oddb out uh in this industry for some reason
all right let's go next nothing so here it's basically asking how do you want users to sign in uh you can use email and
let them authenticate or you can use social media authentication um lean toward email I would just leave email I
wouldn't I wouldn't I don't think we need the other uh is that just showing what it looks like um ah it's not asking me
to sign in it's saying this is what it would look like yeah so the the subheading says choose how users authenticate you
can change this later so that's okay okay like that's saying here's what this is for um I think that that could be a
little bit more clear uh so Dan tus says on LinkedIn uh any advice on how to onboard as a mobile developer to product
people to resolve this I don't understand what do you mean by onboard um I can answer the second sentence which is
normally they will say these things are nice to haves but we don't have the time to do it and I'm telling you that they'
re not nice to haves you you lost me as a customer because you didn't give me good a good onboarding experience and and
I and I see this um talked about in in you know talking about how do we how do we get people you know because they
measure this stuff right they're measuring did you get to this point in in the entire stream um I understand what
onboard means I don't understand what onboard as a mobile developer to product people so that sentence doesn't parse for
me so maybe Dan you could you could rewrite it uh they measure or they should be measuring this funnel of like well they
started it but they didn't finish it where did they drop off and you your goal as designing that part of your product is
you want to make sure people aren't dropping off because if people drop off then you've lost a potential customer and uh
so basically the way I convince people to pay attention to that is this is money this is literally you selling the
product and if you don't then then what else do you care about like especially as as as a startup like that's that's the
major thing is you want to prevent you want to prevent shurn and you want to get new customers and so you don't want to
mess up both those but certainly uh getting people to uh come on to your application um that's their first impression
and you know you are not unique there are lots of choices and so we we want to make sure that people stick with it yeah
okay yeah I it's money period easy I mean ironically it's the easiest thing you can sell you can say look we have data
that people are dropping off here and I can tell you why because people are nervous and anxious and are unsure and
anything like that is going to leave people with with a bad taste in their mouth there going to be lots of people who
just like put in stuff and don't care um but why why cut off people who right next next maybe I'll stop sharing is it
easier for me to do it or for you to take me off just in case something oh it's easy for me to do it okay just in case
something yeah great question Dan okay you can come back all right uh connect your Java codebase use our kit uh well we
don't want to use their starter kit because it's not spring boot or it doesn't appear to be spring boot compatible from
the little research I did um let's let's click on connect and happens so yeah let's scroll down through this SDK uh
update in environment variables so that's really nice that um they hid the secret until you hit the copy button that's
smart um and this is one of those things like if you were sitting alone you know or even in in your your your group uh
Ensemble um it wouldn't matter because nobody there is cares about exposing that information but I like copied um hey
dud so let's see so uh so tells us what the host what the redirect is um and what the logout redirect URL that makes
sense uh the client ID that's public so that's going to be sent along um so this is interesting it's and again this is
making it you know it sort of again clear that they don't understand Java users because they have an at post construct
which leads me to believe that they're using either Jakarta or spring boot but then they have a component scan and I
don't know if that's a spring boot component scan uh it looks like it um but then it like but this is saying nothing
about spring boot like so there's there's just not enough information here about you're telling me post instruct and
you're telling me component scan these are not Java things these are some either jaarda e or some other kind of thing
and this is just you're not telling us what how to use this thing properly so uh let's skip past this because I think
that um we want to go uh and look at some of the the details and some of the authentication stuff because I think since
they support um standard uh oidc which is uh open ID stuff um we can just use the Standard out-of the-box Spring boot
ooth support um so let's click over on on are some of the keys and and they are hiding the client secret which is great
um the call back URL that's automatically set up uh log out so all um I find that amusing that they ask for user first
and last name we've already that um does that mean it doesn't collect names at see yes so if they're so if they're
signing up with with email um then yes that we wouldn't we wouldn't ask them for their for their name with that
unchecked I mean it doesn't mean that our app can do it but it means they won't it means kinda won't do it right um
which makes sense because uh right now it's set to use kind's own signup screens the the that toggle above it I don't
know what's what's with these modern kids today like what whatever happened to checkboxes it's all these toggles that
that are all fancy and I'm like what's wrong with tech checkboxes I'll tell you what's wrong with checkboxes people are
misusing them but anyway that's a separate brand um so let's see uh I think all this stuff was sort of preset when we
when we went through the the initial wizard um so if you click authentication yeah I don't know why I guess we didn't
enter the Java app you want me to go back and do it um yeah yeah glad I have a save button I I know like there are some
uis where everything gets autosaved and it's like I'm never sure if anything actually saved so I I'm an oldfashioned
save button I think is more Comfort comforting to me um so do we want email password or do we want password lists looks
like you can do both interesting but implies it let's see what happens when you click this one no so this is terrible UI
this is terrible this is terrible this implies that you could have both and you cannot this is really why is this toggle
thing here I know I'm I I I ran I wasn't trying to trigger you no I know I I just I'm just like what the heck is this
toggle doing there um it's terrible uh but anyway do I know my preference is I actually really hate password list mainly
because when I'm on like um uh a mobile device it's actually it it it h Works only half the time um because I have to
switch over to my email app and I click it and then it sends me to somewhere else and it doesn't actually log me in and
or leave me where I where I kind of wanted to go so save yeah I was leing toward password tokens um I don't think there'
s anything tokens that that we need to to look at uh so these are yes jeck Jeff radio buttons yes or I mean I'm fine
with like the big boxes but making it clear that like you click on it um and it's really not clear that you click on it
um but yeah like these these are the things that people get frustrated with and the last thing you want like is if
you're trying to sell a product is to frustrate people who haven't paid you anything yet because then they're going to
be like well what happens if I actually start paying you are you GNA frustrate me more um token I think that's I think
that's it here um what I found interesting when I was looking through the docs the other day was uh the place that I
found where um kinda is uh ooth 2 compatible was under migrating from from ozero and uh I actually couldn't couldn't
find it anywhere else anywhere else um I thought that was kind of surprising uh because one of the things that that um
oidc gives you is uh an easy way sort of configure all of the stuff that we have to configure uh with with basically
open ID so open ID is a standard that's kind of incorporates ooth to to provide um basically just the authentication
part so a lot of times people use um ooth just for authentication and not not uh to supply any authorization information
so for example when when I use GitHub all I know is is I know you know you're you and that's all I care about
authentication I'm going to manage what you now have access to myself and so that means you're just using uh GitHub or
that other service for for authentication um kinda though of course uh supplies both authentication and being able to to
manage users inside of its app um and give it permissions there uh and then then you just get side excuse so what we
actually um we want to figure out uh with Spring Security um what are the things that we second so um do you want to
share your screen you're looking at stuff that yeah I'm screen so spring boot uh more specifically the Spring Security
part of of spring of the spring framework uh has a way to configure basically O2 login and so O2 login means um it's
going to handle uh this multi-step round trip to the the server to basically log authenticate so uh so this thing called
oidc is basically open ID connect and so what open ID connect does um is uh make it even sort of easier to to to set up
uh I think what we want configuration so there's a number of ooth client oo resource servers that are built into or sort
of preconfigured as part of spring boot uh or sorry Spring Security um Google GitHub Facebook X AKA Twitter uh and maybe
one or two others um I've heard it called X Twitter which I thought was a nice way of yeah and uh and so what that means
is if it's if it's a common what they call a common provider you pretty much need to just provide two pieces of
information everything else will just work um if it's not a common provider which is the case for for kinda so they use
the example of OCTA here um you provide the name of the provider and then you provide the provider details so this is so
um so for the common ones it already preconfigured this stuff for us we'll have to fill this fill this in is that also
in that list that we saw on the kinda website those properties I think uh most of them not all of them it had the client
ID in secret um and I believe it had a couple of others but they weren't exactly of of the type expected by by yeah so
it has host but that's not enough uh redirect yourl is okay the post is log out redirect URL is is sort of irrelevant um
so we need these two client ID and client secret so we'll get those um what we need to provide is uh where do we go for
authorization um where do we go to get the token so because there this multi-step round trip for oo basically we
redirect you to them you sign in as the user um that then calls back to us with with a successful thing and then we call
and say okay now give us uh I have a uh basically give us details about you and other stuff that that happens in
profiles and all sorts of uh all sorts of stuff so it so weirdly enough like this should have come up in my search for
oidc uh so this is the open ID configuration if we actually hit this um and I'll hit this offline uh we can basically
get a get a bunch of information um which might be all we need because I believe I haven't used the oidc oidc uh stuff
it that's more details want this and so where do we set that is what I'm looking for I have to say Spring Security docs
are less than like it's one of those where you have to know a lot before you can figure out what what to find um so what
I'm looking for is uh this well-known open ID configuration can can help us get stuff configured um but I don't know
where we' where we do that in uh in Spring Security so we'll have to to we have to search well known see uh to get a
client but what I was hoping is we wouldn't all and sort of this is the problem with sort of reference guy is like
here's what this thing is but I'm not going to tell you in context how you might use this for for login because what we
want is we want we want to delegate all the um yeah that just gets us to the open ID docs uh so an oa2 client is useful
if we're g authorization because then we can basically take that and make a request to the resource server uh to say for
this user what what authorization do they have um but I don't want to do that I just login so I think what we'll have to
do is is is uh use this mechanism um which I feel like we shouldn't have to do but um I don't want to spend a lot of
time right now on on stream figuring this out uh so uh let's see if we can basically get get these these properties so
I'm going to switch over to your to your screen because you're going to want be the one creating this give me a link us
in private chat Discord private chat I just saw you got the dark mode thing going on if you want the light mode you can
click it in the upper right is it a spring thing yeah spring box thing yeah and it's another slider I don't mind sliders
for that um I do mind the way kinda does it uh the sun looks like a setting gear yeah it does it's it's it's not as
sunny as it the other problem with with with that is like it shows you what it currently is but it doesn't tell you what
it might be if you click it so it's it's a little bit uh one of those you have to you have happens um all right so let's
uh why don't you grab that that yaml file and we'll create a we'll basically copy that yes just plain file they don't
have yeah just PL file um yo I love how this it look like I didn't spell that right looks right to me okay you know
sometimes that happens you're like look yeah yeah what uh so let's replace um on line six let's replace OA OCTA what
however they um are you waiting for something yeah you said replace it with uh finish oh I didn't hear you say k oh I'm
sorry I thought you were looking something up that so what this is basically saying is now uh it will be uh we'll know
that the name of the client registration configuration and that the provider is is all that so grab the client ID um I
did say it but my microphone may not have picked it up uh let's grab from side um yeah let's go into to the details uh
so let's copy ID and then let's paste that on line seven um how do we deal with this secret yes uh so basically uh on
line eight just just put client secret and you'll go into your local config and and copy and paste that so if you want
to do that now I'll or do you want to do that off screen um local config now we set that up last week but I didn't don't
remember if I took notes of where we put it um what's it what's the F it was it was in uh was the spring boot
configuration so it was in your um in your do config directory off your home directory config spring-boot spring Dev
tools properties file I don't see it okay um you said it was off of way still doing it interesting so on Windows it's
not a dollar sign home on Windows it's percent user uncore home percent oh this is why I don't like Windows anymore I
used to love windows but now like everything is already I was and I was always frustrated because everything all the
docs seem to be centered around using Linux or Mac and so now I'm on the other side of that and I'm like yeah sorry I
don't know I didn't want that work and then under do config under spring boot yep spring boot Dev tools properties yes
that let's hope it which screen it goes on maybe drop me off for a second just in Cas okay there we go they keep me off
screen um so I can get rid of all the super yep and I go back back to kinda copy the client secret right and what
attribute do we assign it to uh so you're G to want it to be that um right the one just called client hyphen secret or
do I need the full you need the entire path got it so um so it might be easier if you did you have anything else you
shouldn't have had anything else in the properties file I deleted the super base stuff yeah and there was there's
nothing else in there right no yeah um I would say just delete it or leave it empty um but what we want to do is we want
a yaml version of that file because otherwise it's going to be painful property oh I see what you mean okay so so yeah
have an empty properties file get out of that and make a new file in the same directory where the properties where the
spring boot Dev tools property file is and Call it spring boot Dev tools yaml got it because this very nested Deep thing
is going to be easier yes so tkes by the way um there's no need to repeat yourself repeat your question I saw your
question I just haven't gotten to it yet um so so no need to repeat your questions okay got the yo file created what are
there and just copy that entire path that but just for the client secret not the client ID yeah you'll want to end up
with basically one one entry yeah for the client secret and then you'll paste the secret grabbed saved we should be good
you can save share screen again um right so now because you have the dev tools uh config properties when we run this
locally it will override the entry here with the one from your private stash as it were um so now we need to to fill out
the the Kinder authorization can we say this yeah you can say whatever you want then um so the authorization URI be
should I go back to the uh yeah it settings uh let's go back to the quick start because it might have been in that
initial section now scroll down the environment fire bills quite well I'm going to guess what it is based on um the the
well-known configuration endpoint which I just pinged for my for my app and it's going to be the same just the subdomain
is going to be different so uh so let's go back into yaml so the authorization URI is going to be um uh your basically
your subdomain whatever that ended up being this okay uh and then so it's SL oo2 uh and then it's just slash off so
delete the rest of it and just keep the word off uh yep that looks right um the token end point uh just delete the V1
there info uh user info I mean these are all going to be the same domain and there's not going to be a V1 uh like be
wonderful if they abided by uh if if if this match the standards that o open ID says um I'm guessing it is the endpoint
user info URI yeah that's probably that uh so instead of oh really they have a V2 okay it's a V2 um so it's oh2 uh slv2
folks don't version your your apis this way please don't do that there's other ways to do it um and then instead of user
profile it's like why would you do that why would you name your endpoint something other than the standard hey add
around yes we're we're we're setting up kindev for for o um and it is far more tedious than it really should be uh the
username attribute uh sub is sufficient um because that refers to the subject I believe uh and then the jwk set URI uh
um J case ah here it is uh so it's instead of OA uh so same domain then dashn uh and then it's jwks and get rid of the O
get rid of the KS is that right yeah I think that's all we need um so once we have that now uh we should be able to
completely delegate all of the authorization sorry all the authentication um to Spring uh so I have to remind myself how
we do that uh I want to up um do you want to share a screen with what you're looking at that be helpful ah here was no
because I need to I need to direct you okay so we now need to create file same level as application yo or somewhere else
uh same level as the um the startup class the song theme startup so it's in the root of the package because it's this is
now actually Java code okay but of type file no no it's it's Java code okay uh and so this is going to be O2 config like
that ooth two the number the number two ooth and the login yeah yeah it the name doesn't matter this is it it doesn't
care as long as we implement the right thing but yeah right yep agree all right go ahead okay um oh somehow you marked
it as an interface no we want this to be a class it's a public class interesting I think you hit annotate you you you've
hit the uh annotation option when you were creating it really I want to undo it and do it again I want to see what it
was I hit all right oh really come on yeah I gotta do go so addan we're not doing the pixie Grant flow because we don't
need to hide stuff we're doing backend um browser based uh just the the open ID flow I should have put in my oh oh to
login security config uh without a g at the end of logging that's login not logging sorry if I wasn't clear no no that
was just bad typing yeah uh oh and it's not a new file by the way it's because you're in the wrong place oh so from here
no no where the song theme start this is jav so it needs to be right right right right right song theme so it was there
yeah yeah okay new Java class yes two of the great ones it works yes oh it must the arrow must have popped down to
interface yeah yeah I see what happened now okay all right there we go much better um and let's we need to throw a
couple of annotations on top of this class so it's both at configuration configuration uh and then we want to enable web
security so once we do this secure uh are you sure or is it called Web is it called enable if okay so what security
config yeah enable web security why is that not popping up for you so just type it out just at enable web security uh
with a no s after web the other s yeah uh oh we might not have it in our pom file that's that's why um because we didn't
turn we didn't actually uh include that dependency because once you include then everything actually by default if you
do nothing it becomes basic authentication uh and so we don't want to do that so uh let's go back to our pom file it's
probably in there just comment it out and look for security yeah so we don't have it uh so let's go add it then um so if
you scroll up in the Palm file to near the top of the dependencies see where it says on line 19 edit starters click on
that let's go find security open that up and we want Spring Security and OA to client sweet and it'll go download
dependencies and integrate stuff and initialize it and index it and okay great so now if we go back here that should be
available yep yep there it is awesome sweet uh I think we can just use the standard config um so uh inside the class
let's we're bean and we're going to say the method is uh public and what this does is it configures what's called a
security filter chain do I call it security filter chain yes that's the type uh so it's a type so it's class security
yep that one there it is yep uh we can just call it the method name filter chain and then the parameter it takes is HTTP
security so upper h lower the rest all right that one yep and we'll just call it HTTP and this throws an exception so
outside Y and so inside this we can just say HTTP Dot and they'll be authorized uh HTTP requests so you can type click
that uh and in there we basically give it a Lambda so we'll call it um so type the word arrow and then uh we'll put this
on a new line to make it easier to read uh request sorry authorize any request okay that's it uh and then outside of
that before you before the semicolon on a new line uh here's where we'll tell it how to do login and so we say do ooth
to lowercase uh no you need to be outside uh it uh Alt J no don't tell close so at this point yes new line dot to and we
want uh login and just say uh with one uh and then on a new line after so build no you had to write the is that's it so
what this does it basically says Hey for any HTTP requests um you're going to authorize you're going to want to be
authenticated and the way we authenticate is with O2 and you're just going to use the defaults for the O2 login um
there's a whole bunch of other things we could configure uh but uh this should at least trigger um by hitting any page
it should trigger the automatic process for for going through the oath in order to do the login so it'll pop us over to
kinder right so it should be if we hit any page um static or or otherwise uh it will um require uh authentication and it
will then kick off the process of redirecting us to kinda we log in there and then it'll kick us back to our thing
underneath the covers it'll do some back and forth and then uh we'll be authenticated um I expect this this won't work
because we haven't done anything to configure anything on the Kinder side um right but at least we should be able to
detect that we've configured things on our end here correctly I have no idea if it's pronounced kindi or k kinda I um so
at and I didn't see anything on their site that said how to pronounce it which is kind of funny I always think like you
should tell folks how to pronounce your company's name um so aderin it might be Ki I say kinda because that's what it
looks like to me uh probably a good time for us to take a break true it has hour and then when we come back we can see
what's broken with this stuff I have I have such low low expectations because this stuff is this is so much harder than
it than it needs to be um and again it this part is is I like this should be in the docs for for for kinda like here's
your application yaml here's your O2 security login config and that's it and and like even providing a sample spring
boot boot app would be nice um but they have their own thing and I don't know what what the heck that's all about so all
right so we'll take a break um five minute five is works for me yep uh so we'll take a 5- minute break and when we come
back um I'll also address some of the questions that have that have piled up so stay that all right uh so let me go back
and and answer some of the questions that have piled up uh so Tes asks uh check the learning path of the official spring
Academy and they ask prerequisites serverless and Tomcat servers um and they teach spring core before spring boot um I
mean you got to know at least you don't have to know uh I find it useful I don't know about the Tomcat servers that's an
odd prerequisite I don't understand I don't think I understand much about Tomcat servers these days um but I think
having an understanding of java servlets at a very basic level I think is important I don't think you have to be an
expert in it um spring so spring Boot and spring that you learn the pieces of the spring framework I think easiest by by
doing by learning spring boot so um I don't know about the details about uh about that that path if you have a link link
to it I can I can go look at it uh later um but this again is an excellent question uh to be asking the Discord um
because then uh it gives folks a chance to respond and you can post links and and things like that so uh there's an
entire Channel dedicated to Spring boot uh spring framework uh so um if you want to follow up on that I I uh recommend
that because then it's not just me answering but other folks who who know um thought there was another question oh uh
watch Alan hulls talk about no estimates again have I watched it um I personally haven't watched it uh Mike I don't know
if you've seen Alan H's no estimates presentation um if you've got a link link for it uh uh go ahead and share share the
link and I can we can look at it offline again great thing to post in for discussion in the Discord um he does post a
lot about No estimates on X Twitter yes um but I haven't looked at X Twitter in a while so I imagine he still is yeah
what I actually prefer is uh woodyz I posted recently somewhere one of the one of the places uh Beyond estimates which I
think is a much better term um no estimates is is intentionally uh provoking I think um in not a great way uh provoking
conversation that leads people to say what you mean no estimates really no estimates and that's not quite what I think a
derail is a conversation so I prefer the term Beyond estimates like yeah there are kinds of estimates that we might have
that we might do that we might find useful um but it would be useful to go beyond that and discover what is actually the
desire for having those and basically go upstream or or left depending on what direction you think about uh to discover
why why do we need those and what kind do we need and what are we using them for and what do you you know so going
Beyond just saying here's an estimate we need an estimate give me an estimate I think this is important and it's telling
that Woody uh who actually originated the term no estimates has shifted in to Beyond es and there's also that really
good uh tool which does um oh my God it's too been too long uh it uses basically uh random Monte Carlo Monte Carlo yeah
yeah Troy m is talks yeah has some really useful stuff in that regard yeah and there's a great spreadsheet that can help
you with figuring out ways without having to estimate each story which is where it's painful yeah and not clearly a
value yeah and I've you know and I've done lots of estimation of lots of stories and I think you can you can do 30 50
stories in in less than an hour you I was going to say if you don't need precise estimates but precise estimates are
sort of a bit of an oxymoron because they're just guesses um and all guesses are educated guesses and uh do need
Precision do you need uh can we do this in this amount of time or do we need to cut scope you know that that kind of
thing and is is is the estimate which is probably like you said better referred to as a guess is is it a commitment as
well right exactly yes that's where it becomes yeah that's where it becomes really problematic it's like oh you
estimated four weeks okay three weeks or it's like you estimated six weeks we don't have six weeks like what why don't
you just tell us how much time you actually have and then we'll figure out what we can fit in right it's like you know
it's like are we playing a guessing game and and I know people you know at management doesn't do it intentionally but
but it's like you have something in mind can we start from there and then work our way backwards instead of us trying to
guess what basically um uh ad asked have worked with other web Frameworks that run in the jbm uh I have I've worked with
gosh five other Frameworks um one of them at least two of them were custom uh um one was uh drop wizard which I used
before I got to Spring boot um drop wizard was nice because it was just what you needed uh was sort of like a mini
spring boot um it tied together a lot of the reference implementation still round uh certainly not as not as popular um
uh I've used the play framework H it's I don't know if I'd even call it a framework uh but I've used play um framework's
a tricky term right it's like if somebody else is doing the dependency injection then then yeah it's a framework uh I do
want to play there's one called rif R uh that I do want to play with um but most of most of the people I work with are
are are using spring boot so do yes that's always great it's like here and then you do nothing with it and commitment
yes I've I've heard of JB is it a framework I mean again the line is a bit fuzzy but it's like do I have to conform to
their stuff or am I calling am I just invoking it like a like a library um but either way I've I've heard of it I haven'
t I haven't really played with there's also vert.x which I've played with a little bit um but uh it all right should we
see if stuff works or stuff fails in the right way to be more accurate sure um here we go I'm back on so we run the app
and uh see how it breaks startup or application app right uh well we re renamed it so you might want to remove that from
the configuration list so click on the Arrow it it I remembered because I said put the config file at the same level to
start the same level yeah so that's uh all right so what's not working top I up uh let's let's bring bring this into
scope so let's dependency oh authorization Grant type cannot be null type h i don't know what they mean by that I mean I
know what they mean but I don't missing does that configuration class need to extend from something well the whole idea
of the configuration is that we shouldn't have to create any class um uh oh I guess we need a couple more pieces of
configuration so um which was not clear from the docs I thought it would have used a default but I guess not so let's go
uh so line8 and a half whoops no back in half uh so we need um we need authorization Grant type so authorization Dash
Grant dtype yep that one code I think that's the stand I think that's the standard I'm I'm guessing but I think it
because it's not a public client so yeah so that should be fine okay okay um and uh Grant types Grant types where is it
supported I'm actually going to have you run this on your end so we can see it um I don't think there's anything in here
that's sensitive okay so um if you basically uh new browser window uh no we can do request uh and you may need to search
for actions because I don't know what under yeah click that that one uhuh uh it's creating a one that's not what I want
um actually just go to the tools window uh tool menu and Go to http one uh and it's going to be song themes do basically
you might even have it in your clipboard somewhere but it's song song themes. k.com or you can just aderan gave you the
full URL if you want to copy that that oh I didn't see the yeah you can just grab the whole thing basically the https uh
song themes kind to wellknown open ID config and so basically what that'll return is is a Json blob of can you say grab
the you mean something in comments yes ah okay I had that window out of yes uh and that accept is correct and so gutter
and we can see all the stuff that we we want want I don't know actually do we want email or open ID I don't know what
those I don't know off hand what those Scopes are um let's ask for both uh so if we go to our application yaml file so
we probably want to minimize this lower one a bit uh and then uh under uh so like eight and a half or sorry n and a half
um scope ID or we could just ask for and let's too um and then we need uh URI so we gave it the grant type I'm just not
sure if the grant type is is thing because if you was if you scroll down in in the bottom uh you'll see a list of uh
authorization so response type supported there um I don't know if that relates to not so I don't know if we should be
code for this for line nine yeah so I I don't I don't know um and their documentation doesn't doesn't say anything about
that or at to well let's try it and see what happens not I'm not seeing oh it is under authorization code okay so that
is the standard it's always hard to tell like what is specific to this Prov provider and what is under the the banner of
the oidc standard uh and authorization uncore code is part of the standard the Scopes are not part of the standard the
username attribute is part of the stand and it's like so it's all this like some of it's standard and some of it's not
and some of it's It's and and it's hard to know which is which without being an expert okay um now what's failed did you
run it again is that why failed again okay far so sorry if you're scrolling I can't read so stop scrolling okay thanks
uh what we what we want to see when we're troubleshooting is what is these where do we start seeing the exception um so
basically from from where we see exception there right there uh that's what we want to we want to see we want to dig
into that um redirect your I suspect that the redirect URI was was empty that uh so line um let's put it after the
authorization Grant type so nine and a half uh redirect is it what we got in the is it highlighted um we want to do
something like that uh so uh I'll I think I know what to type here um you want uh an open curly brace and then the word
bass lowercase and then an uppercase U and the lowercase RL so base URL in in that and kinda and where did you get that
information from I made it up completely out of thin a no uh so base URL uh is um spring know what that is it's
basically whatever the URL of the running application so when we run it locally it will be Local Host 8080 but the nice
thing is when it's running in production it will be whatever the URL domain name and so on is running in production but
it's just the base part of the URL not any path stuff right um so this is the re this is basically the redirect back to
our application so it can uh so the so kinda can send stuff to us um so we basically send this path to them that if they
authenticate then they basically send it back to us um my assumption is we use authorized kinda because we've registered
under the name kinda there on line six um and my assumption is they have to match the documentation does not say um and
this is a perennial problem I find with Spring Security documentation is like here's some stuff but we're not going to
sort of explain what's what is specific to this provider versus what is general that everybody uses and what and how
these names tie together to these other names um so I find myself doing a lot of trial and error um in this case it does
say registration ID but it it's not explicitly called out in in the sample but it is the registration ID uh which so um
so sometimes the information is there just not in in ready to consume way so let's try it again uh I expect different uh
well that is completely different but wow oh it needs to be in double quotes what does the client ID uh the redirect URI
needs to be in double quotes uh and probably the client ID too ID my guess is so yaml is weird um uh in in interpreting
some of this stuff so it's better to put it in quotes if we're not sure what about fine should not must but they yeah
hey look at that all right oh it made it through yes wow so it's now saying that all the endpoints are secured um and
it's it's up and running so let's uh let's go ahead and try it try and what yeah just ship it just hit the play um let's
just go to Local okay great this is progress because we have successfully gone to um kinda and kinda is saying hey this
looks suspicious you're giving us a call back URL that you haven't registered with us um so now we need to go into kinda
and configure the the Callback URL okay uh and you might want to copy and paste what what it says there provided because
that yes we need to to to tell Ked no no this is us so let's see authentication don't ask details so there so it's under
call back URLs yep so just replace that one ah because that's the one that that uh they use in their SD K thinging but
we're not using their SDK I see so we don't need to use that naming no and what we'll do is we'll eventually add the
same one uh sorry we'll add the same path but to The Domain where you're deploying to right um so nice enough here
unlike some ooth providers you can actually enter multiple callback URLs uh GitHub uh they only allow one call back URL
to be white to say this is the URL which means I you have to set up multiple different applications um which is really
an should we do a new line now and get the want yes last time I configured it it only allows one so I basically created
two apps one called the local post version of Embler and the other one called the production version of Embler they are
two separate things um because they only allowed one callback URL they might have changed it recently but as of I don't
know three six months ago nope uh the base URL is is replaced uh at runtime so um it's uh when runtime when it whether
it's happens at the request it might be done as a URI template variable uh is is what I would guess so that it's
probably as it makes the request it's replaced so would production be https yes and uh you can basically just if you
want to put that in the logout redirect you can put that uh as a new line there you basicly you won't want the whole
thing you just want the domain I know I mindlessly Al righty let's save it okay and let's um you should be able to just
go back to the browser we don't need to rerun the app oh just back up and go try it again uh you want to go Local Host
because we haven't yet wow look at that all right so we're making progress now we need to go into kinda and actually uh
I mean we could go and create an account I have no idea what it's going to do we could do that um or we could create a
pre-existing user what do you want to do I would like to see how to do pre-existing user obviously we would know how
this would work yeah um be uh we can go home and see if we can there uh users would be my guess although I don't know
what users that would be yeah I guess we add user okay and I have to have a first and last yeah that's it I don't know
what it's going to use for the password though maybe they have to go they'll have to go through a password reset right
but let's punch it in and and see what happens ah so it's using an authentication code all right now the email came from
song themes oh it's a no reply though interesting right okay I guess I'll do this off screen not that it matters it's
probably one of those yeah it's a one time use code so yeah now I get a createit password I sure hope it's a one time
use code y um W I'm surprised that I'm just looking at the Spring Security docks I'm surprised that they haven't updated
this for spring boot 3 that's a but oh so after I put in you know it said basically create new password oh okay this is
actually a bug in their Docs so uh here I'll share my screen okay so here I can't see one second I got to pull it over
and make it big um okay now I can see so here it it has the example base URL in quotes authorized OCTA but here in the
documentation it says O2 authorization registration ID so here it's authorization this shouldn't say author it should
say wrong it should basically be this okay all right I'll switch back to you then let me grab that actually just I can
just type it authorization so this is actually wait before you do that go back to the browser because you can see the
you can see the URL where' it go there it is so you can see the URL right it's it's basically calling back to wrong so
authorization here like that um and suiga points out also that we need the SL oath too so that base you that that
redirect you is just completely wrong I now want to on oh you using kinda for your other project no I'm using um wow so
this so the GitHub redirect UI different uh did that change because in my configuration my redirect URI is um base URL
uh well let's at least P see see if the correct where did you want me to go to um uh sorry no go go to to the
application properties where you were uh so stick in front of authorization stick 2 I feel like that's wrong but we'll
let's try that um what we can also do uh is we can actually try to hit that end see actually you know what let's
actually try to hit that endpoint so let's um so copy and paste the SL oo2 to the yep and then go to the browser 8080
and Slash and then add that so happens okay so that's good um we'll have to rewi list the correct thing to uh it wasn't
here this is the users home and then work uh I think it's under your right oh wait down here yeah yeah right so let's
replace that yeah okay now uh so now um yeah let's just go to Local Host 880 and let's try to authorize uh can you just
delete the whole thing and do Local Host 880 yeah without it okay sure that's what I'm going to do ready yeah yeah
that's what I did do it and gave 880 yeah it's stuck in a a redirect Loop because uh the URI is still not correct so
what's happening is it goes to to kinda then it comes back but the place it comes back to isn't an unnown thing and
basically then it tries to make it to authenticate on it and so it goes back and forth um I don't know if you can make
the right side bigger by zooming I don't know if you can zoom on on the right right side let find out I guess not gives
no that's for performance appearance not seeing anything for are size so let's do this um I want to try one more thing
be and then we can uh we can we can then troubleshoot using the network console so let's uh you can browser and maybe
one of our viewers can look up how do I make the network console text bigger uh so let's go back properties um let's
change it understand I don't understand what the other docs are talking about because for login this redirect URI is is
wrong um so stick the word login slash in 2 uh other way around want to slash before login yeah I know uh and instead of
code and actually the registration ID is also a template variable even it should be kinda uh we can actually use curly
ID instead of here yeah so replace kinda with registration ID ah and uppercase i for ID y so what it'll do is at runtime
it will place it with the appropriate registration ID which should be kinda um it's the unique identifier which we've
defined uh so let's try this so let's restart the it um before you go uh oh we'll have to change also the call back
because we just change that so right you won't be able to use registration ID on their end no I know okay this way we'll
remember to change it and then what would kinder this is why we shouldn't have done both urls yagy you could delete the
other one and then we can always add it later yeah true we not constantly updating both fail interesting the save is
spinning again do I need to restart the app uh we just restarted it so it should be fine right wow a long time to save
all right so let's open up yeah new tab uh before you hit enter let's open up the network it okay give it a roll are you
here searching how to inrease um well it says it should should work but it doesn't unless maybe you have to have a focus
there if you click uh in the filter on the right side right side well you where you just clicked yeah that's the right
side that's the right side oh I see uh and now hit hit uh zoom in yeah there you go there we go so it had to have the
focus okay yeah sweet okay let me clear it yeah uh where's the button go there it hey h it worked it worked oh my God
that's cool because it had already it had already cached the the login so when it went to do the ooth uh actually let's
let's inspect the bigger right so uh we hit Local Host it did uh a redirect um it r directed us to uh actually we want
to make the initiator column bigger because that's that's the important stuff we can you can make the type column really
tiny column then you can make the initiator bigger and so uh so basically we hit that Local Host it said oh you need to
be authenticated so spring redirected us to um uh kinda with a code and then uh then it did uh and it said oh I already
know who you are so I'm going to send you back to login with the code to confirm that this is the code you gave me and
you're logged in and good sweet and then it looks like it it did a request again because we haven't said we've basically
said every request needs to be authenticated so when it tried to grab the favicon right which you don't have to find it
had to go through the the authentication process again right we were gonna narrow the scope of where authentication now
like oh my God it this but now you know one of us gets to write a blog article on how to configure kinda with spring
boot client automatic registration and Save Somebody two hours yeah Jesus this should this should not have been this
painful but every time I do this it always seems to be this painful painful um whereas if if they had proper if and and
this is totally on kinda they simply did not document this in a way that would have been useful to the majority of
backend Java Vel oper is using spring boot like market share of spring boot is what 60 70% and so you basically said we
could care less about the Java market and that's that's that's too bad for them um so uh it's 12:30 um which was the our
planned uh end time um but we're now in good shape uh for um setting up the the different so now we've got
authentication and so now we have to decide um how do we want to do the authorization so the simplest way is basically
say this page anybody can access it they don't need to be authenticated to access this page they need to be
authenticated and right now you're the only one who can be authenticated so therefore that would be sufficient that
would be sort of like the minimal amount of security we would need in order to deploy so would we would punt on roles
until we had a second person exactly well yeah that would have basically punt until we have somebody who has a different
role yeah right yes yep yep cool all right uh well let's uh I don't know if you want to I mean may as well commit this
um so next time uh and I don't think we've firmed up a schedule for that yet but next time we will go ahead and do that
we'll we'll basically use um Springs uh security configuration to uh and it's what's called request matchers to
basically say for this path of information anybody can can access it um which would pretty much just be for the homepage
and anything off the homepage uh and then anything under under admin we could say no this requires you to be uh
authenticated and so we'll do that do that next wow that was a chunk of time yeah all right folks um but hey it's nice
to get to the point where we get working we ends yeah no no one likes to end on frustration yeah yeah so unlike last
time this time we we are successfully uh authenticating uh everything's configured the way we needed to and we can
finally then move forward uh on on creating the UI for actually importing uh bulk importing our songs so uh that'll be
the first things we do next time so that's all folks so thanks for thanks for hanging out and thanks for the help along
the way definitely appreciate it uh and um as always if you want to be informed of future streams more than just hey we'
re going live messages uh you'll want to join the Discord and make sure you go into the rolls Channel and tap on the
little alert icon under Cod stream alert uh and so is uh and watch out for announcements there um I do also post post on
on uh Mastadon and and Twitter um but those are secondary sources Discord is always the one that's going to have the
most notice and the most upto-date there anything else to say Mike before we we no looking forward to the next step y
once we figure out when that is yes yes all right folks uh thanks for thanks for joining and we will see you next time
