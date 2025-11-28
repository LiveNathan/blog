# Quick Introduction to the JitterChat Project

**Video URL:** https://www.youtube.com/watch?v=Kpd2H9ftMjg

---

## Transcript

hey folks this is Ted M young also known as jitter Ted and this is just a quick intro to the jitter chat project that
I'm working on so this is actually the code for the project and so one thing you'll notice there's a plugin that I have
active called get toolbox and so that's what's displaying this sort of line highlight or what's called a line painter
and it basically the line that you're on it shows as sort of a comment on that line when that line was changed and in
what commit and so what I have is I wanted to do something like that except instead of the information coming from a git
repository or something I wanted to integrate it with the twitch chat so I'm working on a plug-in that does exactly that
that integrates the twitch channel chat into a window in IntelliJ and also allows chatters to be able to do things like
move the focus of the caret to a specific line and make comments on different lines in that file so what I have here is
I'm running the sort of sandbox version or development version of the plug-in that is working so far and so you can see
on the right is the jitter chat window where the chat will appear and I can connect to twitch I won't do that now so I
can say line 18 and it moves the highlight basically the current selected line fat to that line number so I can also say
comment 14 what is draft and right now what will happen is is if I move the cursor to that line you'll see this comment
appear right the comment isn't really in the code it just appears as sort of a higher-level kind of annotation and so my
continuing goal in developing this plug-in is to improve things make it more sort of production worthy do things like
put something in the gutter to show that somebody put a comment there allow you to clear them things like that because
my goal is not only to get rid of an extra window for chatting but also to provide more interaction four or five viewers
all right that's it
