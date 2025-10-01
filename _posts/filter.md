# How Many Filters Are Too Many? Building a Tool to Find Out

This past week I worked on a medium-sized show where, for the first time, I had access to tools that let me generate
many EQ filters quickly and then deploy them to my output processor just as fast. This raised a question I've been
wrestling with for years: how many filters are too many?

## The Old Heuristic

For years, I've followed the L'Acoustics best practice of limiting myself to one EQ filter per measurement. Take eight
measurements of a zone, use eight filters. This approach has several benefits:

**Prevents obsessing.** With a limited filter budget, you're forced to address only the biggest problems rather than
chasing every tiny issue.

**Encourages wider filters.** When you only have eight filters total, you can't afford to use narrow, surgical cuts. You
have to zoom out and shape the overall response.

**Saves time.** In live event production, time is always the constraint. Inserting 12 filters takes twice as long as six
filters, and it's more important to check every zone your PA covers than to perfect just one. You'd feel pretty foolish
spending an hour perfecting filters for a single zone, only to discover another zone has almost no HF due to an
obstruction or mechanical problem.

This heuristic has become standard in my work and teaching. Use fewer, wider filters. Don't obsess. Get the target
shape, not every tiny detail.

## The Temptation of Automation

Then came automation. Apps like [REW](https://www.roomeqwizard.com/)
and [CrossLite](https://www.fmscience.com.br/en/crosslite.php) now include sophisticated auto EQ features. CrossLite can
insert 24 filters in one second—not only faster than I can insert them manually, but in some cases it makes better
choices than me. Similar to how SubAligner considers every possible combination of delay and polarity, auto EQ can
consider every combination of frequency, gain, and width. It can even account for group delay and other factors I
typically never examine.

If you're a purist, you hate this. EQ should be minimal or nonexistent. But if you're a pragmatist who just needs to get
the job done, this is a game changer.

When CrossLite added its auto EQ feature, I started using it on every show. It doesn't always produce the results I
want, but it's quick to try and usually gives me a better starting point than working from scratch. Even with this
feature, I still limit myself to one filter per measurement—partly because of the reasons I already described, but
mostly because every single one of those filters had to be manually transferred by hand from CrossLite to my output
processor.

That manual transfer was the bottleneck.

## Building the Solution

For this recent show in NYC, I decided to build a CLI app to automate the transfer process.

CrossLite doesn't have an API yet, but it can export filter coefficients as a text file, and d&b's R1 software can
import XML files for EQ settings. All I had to do was convert between the two formats. That part turned out to be easy.

The hard part? Reading Windows file paths with backslashes.

## The Backslash Problem

Here's what I discovered: the Spring Shell framework I used for building the CLI app automatically removes backslashes
from string parameters. This isn't Spring being deliberately hostile to Windows—it's actually a deeper issue about how
shells and command-line interfaces handle escape characters.

In command-line environments, backslashes function as escape characters, which changes how the shell interprets the
following character. When you type a Windows path like `C:\Users\file.txt` in a Unix-based shell (which many modern CLI
frameworks emulate), the shell interprets the backslash as an escape character and removes it before the application
even sees it.

In Java property files and many string contexts, backslashes must be escaped (written as `\\`) because they're treated
as escape characters. This is a known issue with Spring Shell—when users type backslashes in commands, the shell
processing layer strips them out before they reach your application code.

I tried several workarounds. First, I refactored the app to use interactive mode, which provides a better user
experience by letting you step through the app's inputs like filling out a form instead of cramming everything into one
command:

```
# Instead of this:
crosslite-r1-eq -i my-file.txt -o my-output.rcp

# You get this:
crosslite-r1-eq

What is the input file path?
my-file.txt

What is the output file path?
my-output.rcp
```

Unfortunately, interactive mode didn't solve the backslash issue on my Windows 10 machine. The only workaround that
actually worked: ask users to first navigate to the folder containing their CrossLite file, then run the tool on just
the filename instead of the full path.

It's annoying, and I wish I knew a better solution. The proper solution would be to use forward slashes, which Windows
accepts as path separators and Java handles cross-platform, but that requires users to manually convert their paths or
remember to use forward slashes—not a great experience for a quick command-line tool.

All of this would be easier as a web app, but production audio networks rarely have internet connections. I could build
a desktop app that emulates a web interface (like I did for Console Whisperer). If there's interest in this tool beyond
just me, that's probably the direction I'll take.

## The Windows Defender Problem

Another issue I discovered while making a demo video: Windows Defender immediately deletes the `crosslite-r1-eq.exe`
file after download. This is a false positive detection, which commonly occurs when new or rare software behaves
similarly to known threats, or when executables are unsigned.

I had to add my Downloads folder to Windows Defender's exclusion list just to test the app. This doesn't feel like the
right solution. The technically correct solution is probably for me to get a code signing certificate, but for small
tools and demo apps there's probably a better solution than exluding entire folders from Windows Defender.

## Lessons Learned

Looking back, I underestimated the complexity of building a production-quality CLI tool. I thought GraalVM would make
everything simple—just compile to native and ship the executable. In reality:

1. Windows file path handling is genuinely challenging when building cross-platform CLI tools. The backslash escape
   character issue is fundamental to how shells work, not a Spring-specific problem.
2. Unsigned executables face significant distribution challenges on Windows. Users won't download tools that Windows
   Defender immediately quarantines.
3. GraalVM Native Image is powerful but not a panacea for distribution.

## Looking Forward

Despite these challenges, I successfully used the tool in a production setting, and it works. The core idea is sound:
automating the transfer of EQ settings from CrossLite to R1 removes a significant bottleneck in my workflow.

If there's interest from other system techs and sound engineers, I'll likely rebuild this as either:

- A feature integrated into [Console Whisperer](https://youtu.be/Kpb2Zm6Bd8A)
- A standalone desktop application with a GUI
- A web application (accepting the internet connection requirement)

Until then, the command-line version lives
at [this github repo](https://github.com/LiveNathan/crosslite-r1-eq). It works, but use it with the
knowledge that you'll need to configure Windows Defender exceptions and navigate to your file directory before running
it.

Back to my original question: how many filters are too many?

One way to answer it might be an AB listening test. Compare the results of four filters with 24, for example. Until
then, I'm glad that I now have a workflow that makes it easier to experiment and find out.