Let's do a personal blog post, and that's basically an update on where some of my projects are at and some of the things
I've been learning, and I guess where I'm at personally with some things. So I guess I don't know how exactly to
structure it, so I will just talk for a little bit as things come to me, and then maybe you can help me decide exactly
how to structure it and what would be an interesting way to write it so that it is interesting and maybe kind of fun for
people to read. So the big project that I've been working on this year, the one that I spent the most time on at least,
is Gain Guardian. And it feels like it's still just kind of stuck in the mud. I felt like we got pretty far with it, and
I guess, you know, from a higher level perspective, I should say that it's stuck from a technical perspective. And that
technical perspective is that we cannot do successful demos. And it has been the funny story with this product because I
thought that we would have demos within two weeks, and here we are six months later, and we still can't make successful
demos. Which is disappointing. There is one critical challenge that we are facing, which is how to actually apply the
algorithm. And that's essentially on the subject of convolution. Oh, shoot. Um, here we go. And that's why I've been
writing a few other blog posts about convolution to try to teach myself more about it and see if I can understand it
better. So I have reached out to a couple of other people to try to help with this. And that's definitely sparked some
ideas, but no solutions yet. And the problem is that I kind of went broke this summer while working on this project. And
so decided that I needed to steer away from it for a bit while I figured out some other projects that would have more
positive cash flow for a while. So I still think it would be fun to work on Gain Guardian, and I do want to see it be
successful. And I think it's an important project. And I think it could be a great product that actually helps people
and makes things sound better. But it's just the road ahead is so unclear. I don't know if it's going to take another
year or another 10 years. So I am kind of, I guess, losing motivation and losing some hope of that product ever seeing
customers. Then there's Console Whisperer. Console Whisperer had some energy around it initially. And I guess it still
does. It's for sure one of the easiest things that I've ever marketed because all sound engineers use mixing consoles.
All sound engineers have some interest in them. And anything that has AI attached to it has some interest right now. And
so anytime I meet another sound engineer, I can just say, hey, do you use mixing station? And if they say yes, then I
say, great. Do you want to check out this product that I'm working on? So that part has been nice. And I have about 10
people that have signed up to be early adopters and test out the product. But development has also slowed down on that
due to some technical challenges. Namely, that as soon as I had to reconfigure it into a client server architecture, now
everything feels like it's twice as hard or more. Because now every time I work on it, all these different things have
to be considered. So I don't know if I want to tell a long story about that right now. But it's just harder to work on.
And also just the cross-platform. Yeah, there's just so many little... I want to say painful, but it's really, I guess,
interesting. Little interesting challenges with it. Which, if it was just one of them, it might be fun. But like, I
don't know. Just a lot to work out, you know? Like there is the non-deterministic nature of the LLM and trying to figure
that shit out. And then there is the cross-platform nature of a desktop app. I've never worked with a desktop app
before. I've never done kind of cross-platform stuff before. And so I keep publishing updates and then hearing that they
don't work on this platform or that platform. And then I got to go check it out. And so there's all... I have to do all
this new manual testing and understanding, like, why some things don't work on Windows. And some things do work on Mac,
etc. And honestly, it still just feels like the whole working with LLMs thing and frameworks and technology that I'm
using is still nascent. How do you spell it? How do you say that word? N-A-S-C-E-N-T? Nascent? Nascent? Nascent? It just
feels like it's still early. You know, a lot of the shit just doesn't work very well. It's like, yeah, you can do all
this stuff. You can add tools and memory and functions and you can do retrieval augmented generation. None of that shit
works great still, unfortunately. Yes, you can do all that stuff, but it's just super... I don't know. I shouldn't say
super. It's fairly flaky. There are a lot of issues. As I wrote in my last blog post, if you look at the Spring AI
GitHub repo, there are like 176 open issues or something like that. But so, and the thing that I was testing is that,
yes, you can do tool calling with the LLM and that'll work a little bit. And yes, you can do have chat memory so that it
feels like a dialogue. But then as soon as you combine the two, then things start breaking and not reliably, but just
every other message maybe. And then you have to like fight with the LLM a little bit and say, hey, you didn't do the
thing I told you to do. So that part in itself is frustrating. And then on top of that, you know, learning to deal with
the client server architecture and desktop apps. And I'm trying to use VODEN, which is a web app technology, to do a
desktop app. So I don't know. It just all feels a little bit painful and like I'm trying to push a square peg through a
round hole. So I'm meeting with my coding coach on Wednesday and I'm hoping he'll have some insights around that. I'm
also thinking about maybe doing another proof of concept where I try to get a local only LLM version of it. But it just
feels like everything would be nicer and simpler if I could only do a web app or only do a desktop app. But the client
server architecture thing feels kind of painful. So I still only have one. I still only have one. I still only have one
customer for Console Whisperer. And what I'm doing is slowly going through each person that's signed up to be an early
adopter, and I'm testing their use case and then following up with them. Now, I fucked that up a little bit because I
haven't been taking great notes on where to follow up with people. So for example, I finally completed one person's use
case and tested it out, and then I went to message them about it and realized that I do have their email address. But I
feel like in modern life that is very weak because I just feel like email is not very reliable, especially if you've
never communicated with someone before. I feel like there's a 50-50 chance that just any email that I send to them will
just never be seen, either because it'll end up in spam or they're just one of those people that doesn't check their
email. My brother is a great example of this. You would think that personal emails from your brother would get seen
pretty quickly and replied to. And anytime I send an email to my brother, I have to call him or text him about it to get
him to see it. So just an example of the unreliability of email. So it's critical when I talk to each of these people
that want to test console whisperer that I write down what channel is the best to follow up with them at. Otherwise, the
whole thing is kind of lost. So that's a minor challenge right now. And I'm wondering if maybe I should kind of skip the
part where I follow up with everyone one by one and just jump to, you know, making it publicly available and just reach
out to them all in mass, you know, so that I don't lose some of this momentum. Because I think it's already been over a
month since I talked to the first person and so they've probably forgotten about it by now. But you can do a lot with
the product already. So it still has some bugs and it's a little bit flaky. But at this point, I think you can almost do
anything, anything that you can do on mixing station, you can also do on console whisperer, which means that you can
tell it to, you know, name channels one through 128, RF one through 128, and it'll change all the channel names faster
than you could. And things like that. And things like that. So getting close to it being like a real assistant that
could help you with stuff. I'm still not sure what to do about the pricing. I thought it would be fun to do kind of QLab
style pricing. And so I've been offering early adopters. I discount on a lifetime price. And then my friend Pavel warned
me against lifetime pricing and said that it might be better to just do give people the give people a discount on like
an annual price, like for the first year or something. That makes better sense from a business perspective. And actually
might make more sense for users since they don't even know if they're going to want it after a year. I don't know.
That's a minor note. But just another question on my mind is how to handle pricing, especially at the beginning when I
don't know how much the thing is worth or how much it should be priced at. And the big news is that I've started working
part time at Squarewave. Squarewave is an Australian company that supports production AV companies, specifically
production AV companies that use an app called Flex Rental Solutions to run their business on. Flex Rental Solutions
helps manage inventory and do quotes and accept payments and attempts to be one of those big applications that you can
attempt to run your whole business on. I believe it falls under the category of ERP. Not totally sure. Not totally sure.
But it's I think Squarewave started out as just consulting and then got into software. And one of the things that they
do is create custom reports that you can import into Flex to do things like show, you know, generate a profit and loss
report or, you know, things related to manifest for trucking. And logistics and lots of other things like that. I don't
even know yet because I just started. So last week I did my first week of training so that I can join the team that they
have of people that create custom reports. And that's been really interesting. So improving my knowledge around SQL and
learning this product called Jasper Soft Studio, which is what is used to design these custom reports and then outputs a
file format called JR XML, which I haven't confirmed but looks like a superset of XML. And I immediately had some
product ideas just getting started at Squarewave that I might investigate in some future blog posts. So for example,
they use an app called Gather for internal meetings. And it's pretty fun. And it's pretty fun. But it also seems
relatively new and has some problems and bugs. So for example, you can do meetings and you can record them. And then it
will afterwards give you the recording and the transcription, which is great because since it's internal and it knows
who you are, then it already knows your name. So it has the speaker names, so it has the speaker names in the
transcription. But since it's fairly new, you can't do, I don't know, it just doesn't have a lot of features. Like you
can't record for more than three hours, which it doesn't tell you about. It just lets you keep recording, but it doesn't
tell you that it's going to stop at three hours. You can't download the transcription. And it's not connected to the API
yet. So I would like to create an automation, for example, that after every meeting, it will get the transcription and
the recording and put them into my personal folder in the knowledge base that SquareWave uses called Slight, which is
S-L-I-T-E. And it would be cool to just automate that so that anytime I want, I can go back to the recording of that
meeting to see something that I may have forgotten or missed. This is especially important in these early days where
people are just throwing all kinds of new shit at me that I don't understand. So I did make a little script that helps
clean up the transcription by doing things like removing all of the timecode and creating aliases for people's names to
just kind of reduce the overall character count, which is important for, you know, being able to add more context to an
LLM. But also, just would like to have an automation that handles it all because it does take a little while to do all
of those recordings one by one. So I might look at that. It would be, it would be a lot easier if gather would expose
access to these meeting recordings through their API, because I see that Slight also has an API, but I don't know, maybe
there's another workaround. So, yeah, let's just take a minute. So far, make sure you have to go I see some real things
around the phone you can technology. I would also like to see, just on a personal note, if I can set up a way to create
these JasperSoft JRXML files using Java, using a TDD style approach, and maybe never have to use JasperSoft Studio.
There's nothing necessarily wrong with JasperSoft Studio, but I'm just not very interested in front-end design that
much, and I would just rather figure out. That's why I like Vauden so much, honestly, is that you can do everything from
Java. You never have to touch JavaScript, and it just handles a lot of design stuff for you. So I'd like to see if I can
come up with a similar way to do that for Jasper Reports in Java. I found a framework called Dynamic Reports that might
allow me to do that, because I think it would be a lot more fun to work on this job if I could figure out a way to do it
with Java and with TDD, which is always a more pleasant experience than just poking around in a GUI. Oh yeah, just
thinking about where to go next with some of these projects. If I am now spending 20 hours a week working for
SquareWave, and I have about 20 left, then how much of that should I spend on Console Whisperer? How much of that should
I spend on Gain Guardian? Should I set some of that aside to work on new projects? That seems like a good time to
reassess all of that and think about what to do moving forward. Thank you very much.