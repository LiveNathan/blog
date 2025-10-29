Over the last couple of weeks, I've been doing some research into power calculations for production AV needs. All of my
professional experience is in pro audio, and historically, I've always tried to avoid anything that doesn't have to do
with whatever my specific focus is. Because I always prefer to go deeper on one subject that I have some familiarity
with than to have a surface level knowledge of anything else. So I always wanted to go deeper on sound system design and
calibration, and would ignore learning other parts of the craft, like power and rigging. But of course, those are all
critical elements to production AV. And with hindsight, I see now that there's not actually a lot of room for hyper
specialists, or probably the word hyper isn't even necessary there. But just specialists in general in production AV,
because it's just not a huge industry. So I don't know if you can make some comparison there with the medical industry.
But one of the things that I took away from reading the checklist manifesto is that medical doctors are very specialized
now. And that is one of the reasons that it can be so expensive. But I can't remember now how to explain that. I would
have to go back and reread that section of the checklist manifesto. But maybe there's some connection there between, you
know, I assume every industry has this, where, you know, as it grows, it becomes more and more specialized. So I think I
always wanted to be a specialist. And I always wanted to avoid being a generalist. And I think that has to do with me
wanting to be a special ego, you know, like this and, you know, do something with my personality. Like this is the
special guy, Nathan, that's really special. And he does this one thing really, really well. And that's what he's known
for. And I think that's what the world kind of tells us to do is to, you know, hone our craft and get really good at one
thing. So that then that's the thing that you can help people with really well. And you can deliver a lot of value. And
then you can charge a lot of money for it. And then you can enjoy doing it. And people will enjoy paying you for it. And
things are supposed to work that way. But I don't think it ever really worked out for me that way in production AV.
Because I kept trying to promote myself in those ways of being like really good at this one thing and get better and
better at this one thing. And I kept getting more and more education around that thing. And it never got me more work.
It may have gotten me a little bit more work as an educator, but not really. And in terms of production AV work, I don't
think I ever got more work because I was a specialist in sound system design and calibration. In fact, I think I was
only ever once hired in my life to do just that job. Maybe twice, you know, in 25 years. So I don't know if there's a
conclusion that we can draw from that, except that maybe smaller, less developed industries like production AV, where
you kind of need people who can do a lot of different things or be familiar with many different fields, like not only
some specialty within audio, but everything that that touches, you know, so the rigging and the power and networking and
things like that. And so probably the that the industry needs more generalists and less specialists to get the job done.
And all of that is, I guess, a long way of saying that I never learned that much about power. And I have taken some
courses in it. I took Scott Adamson's show power course a few years ago, and it was really good. But then I didn't
really use that information often afterwards. And so I forgot a lot of it. And then a year ago, I was doing research for
an app I was trying to build for commercial AV integrators. And one person that I interviewed told me that what I should
really build is some kind of an app that would do power calculations for people. And it would maybe take in all of the
design elements from Vectorworks or AutoCAD or something and add up everything that's in a rack. And so then you could
say, OK, this rack has these specifications related to power. And then that's what you need to give to somebody else on
the team that's handling that. That actually sounded really cool. I couldn't find anybody else of the 50 people that I
interviewed that wanted that. So I didn't move forward with it. But then a couple of weeks ago, I guess three weeks at
this point, I started working at Squarewave. And one of the things that I pitched to them is that they should make a
custom report for Flex that would do some kind of power calculations. And my thinking was that you would want to do that
in production AV so that you could size a generator or make some specifications for what you would need in terms of
power from, you know, the hotel ballroom that you were going to rent or something. I know so little about power that I
don't even really know the right words to use. And, you know, it's especially funny since my dad is an electrical
engineer. And I remember as a kid, he tried to teach me some things and he gave me some books and we talked about it.
And then I forgot a lot of that stuff. So, you know, maybe me avoiding learning about power and electricity is, you
know, one way to know what what the right verb is. And, you know, children always try to do something in spite of their
parents. You know, children never want to be like their parents. They want to do the opposite. They want to go to the
other side of the world and do something completely different. So maybe that's one way that that happened for me. So,
yeah. So it was funny that I pitched that to Square Wave because it was an idea that I got a year ago and I thought,
hey, this is, you know, one idea. You guys should make this thing. Of course, I didn't consider that now that I work
there that they would make that my responsibility. So it turns out that that was an idea that somebody else had already
had at Square Wave related to power. So then they just attached my name to it and said, hey, Nathan, can you do a little
research on this? That's I think they didn't ask even ask me to do that. They just asked me to fill out the form that
gets the project started. That's like the description for the product. They probably thought it would take me, you know,
like 30 minutes. Of course, that's not how I do things. I I go way too far with everything. So I think I at this point
have called four or five people. I've done some discovery interviews and then I did some research, posted on Reddit and
some social media places. And so what I think would be fun to do with this next blog post is to document some of the
stuff that I learned that might be helpful for other people. And I could also share some of the products that I found.
Like there was that guy that messaged me on LinkedIn who already has built a nice little web app where you can just
input your stuff. Pretty much the same as like using a spreadsheet. And then somebody on Reddit sent me a demo of the
kind of spreadsheet that they use at work. So I'll try to list some of my takeaways that I learned from all this
research. Um, and then you can help me fill in the rest by pulling out the most important stuff from all of the
research. And that way, even if this doesn't turn into a product or a real custom report that people can buy and use, at
least some of the research that I did will maybe help other people who might be looking for this information. So I think
my biggest takeaway in terms of the product and the product design is that, uh, demand is not really in sizing a
generator. Um, most people don't seem to care about that that much. Uh, nor do people really care so much about
overloading a distro or a cable or a connector even. Um, what I discovered is that most production AV companies have a
really small number of distros, maybe one or two or three. And they all know what they are. They have their 100 amp
distro and their 200 amp distro. And so if it's a small show, they use the small one. And if it's the big show, they use
the big one. I don't even know if I'm using the right numbers there, but that's just an example. It's just such a coarse
thing that everyone just knows, I think. And I don't even know if they put those on their quotes in Flex. I'll have to
take a look or do some closer research. I don't even know if people put that in their inventory. Um, what I immediately
discovered that people did maybe need some help with, because it's what people are doing currently manually with
spreadsheets, is balance. Uh, that is balancing the legs on a three-phase power source. And, again, I don't know if I'll
get all of this correct, so you'll have to be my technical editor and help me fill in some of the missing technical
details. Um, but the way I understand that typical show power happens is that there's some sort of service that comes,
let's say, from a hotel, a hotel ballroom. And that is three-phase, probably cam lock. I don't even know if we need to
talk about that, but three-phase power. And I don't remember why it's three-phase, and I don't remember what the voltage
is, maybe 220. But the important thing is, is that you connect those three phases to your distro, and then I think that
means that you have three legs of power to draw on. And then it's your responsibility as the user, then, to make sure
that you balance out the things that you plug in to that distro, so that they're balanced across the legs. Uh, and it
took me a while to find out, and I still don't quite understand, but the worst-case scenario, the thing you want to
avoid, is a situation where you are highly unbalanced, and then that neutral might get unplugged. I think that is the
thing to avoid. That seems, I've never heard of that happening, that seems really unlikely, but it is possible. So, if
things are unbalanced, and the neutral gets unplugged, or burned out, or fails, then, all of a sudden, I think you send,
you can accidentally send way too much voltage to some devices, and destroy devices. So, I don't know if that creates
unsafe working conditions for humans, but I think it can just destroy equipment. So, what most, so what I, I talked to a
few of my friends that are lighting technicians, and what they told me is that they're typically just doing that on the
fly, in the field. So, as we're plugging stuff in, I know my friend Jordan is just sort of doing this in his head, like,
okay, I'll plug all these things to L1, and then all these things to L2, and that's with a single distro for, like, a
smaller show. And so, people are building spreadsheets, and little web apps to help them do that, where they just list
out each device, what is, power draw is, and what, and then they sum all of those per leg, to make sure that they are
balanced, and not too far off from each other. Now, I don't know how far off, too far is, I was planning to set a
default of 20%, and so that is the biggest thing that I was planning to do with this report, is to help people do that
in their quotes, or in their proposals, or in their pool sheets for equipment, is to balance that stuff so that, you
know, as they're planning their show out within their quote, they can plan that out, and then print this custom report,
and then make sure, you know, have some confidence that they have kind of a power plan. And a lot of people don't need
this. It's interesting that, I guess there's like kind of a middle market where they might need this. There are, you
know, there are very small shows where it probably doesn't matter. There are very big shows where you are going to have
someone who is doing their lighting, doing the lighting design, and maybe the entire design for the show in Vectorworks.
And Vectorworks has tools for helping you make that power plan anyway. So then you have someone who's already
responsible for that, so you don't really need to do that in Flex. So then it's probably a lot of medium-sized shows
where you're not using Vectorworks to design your show, and it's big enough that you do want to do some due diligence
around this topic, and that is where it might be helpful to have this kind of support built into Flex, so that you can
work with it in your quote as you're building your show. So, yeah, I'm not really sure what else to say about it. I
mean, I guess there's a lot of other takeaways that I could say about power, but maybe it would be good to just focus on
this idea of balance and maybe try to simplify that understanding for myself and even make some kind of a diagram so I
could see, you know, like on a medium-sized show, yeah, maybe we'll just follow the use case, like on a medium-sized
show, what is happening with the power? When you have a single distro and all departments, lighting, video, audio,
scenic, whatever, are all using it, then what do you need to do and what will happen if you don't do that correctly? So
if we're going to make this blog post mainly about how to balance what you're plugging into a distro across three-phase
power, then one of the important, interesting, critical questions is how you get that value. Do you use the max value or
some other value? So it would probably be good to look at some examples. So I think I mostly did research into audio
examples of like power amplifiers and stuff, and for that there's this idea of typical draw, which I think is related to
one-eighth something pink noise, I don't remember, but maybe it would be good to look at a few of those things so I can
even train myself, like this is the value you should use for an audio amplifier, and this is the value you should use
for an LED lighting fixture, and this is the value you use for a video projector, and stuff like that. And then I could
do kind of my own simple calculations to show how that would work. Yeah, so maybe that is their focus and refinement for
this blog post is this idea of balancing three-phase power, what the motivation is, why you would want to do that, and
then step-by-step exactly how to do it. Thank you.