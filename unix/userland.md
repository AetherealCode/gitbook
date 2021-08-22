# userland

## userland 

## [\#](https://p1k3.com/userland-book/#a-book-about-the-command-line-for-humans) a book about the command line for humans 

In the fall of 2013, [thinking about](https://p1k3.com/2013/8/4) text utilities got me thinking in turn about how my writing habits depend on the Linux command line. This seems like a good hook for explaining some tools I use every day, so now I’m writing a short, haphazard book.  
This isn’t a book about system administration, writing complex software, or becoming a wizard. I am not a wizard, and I don’t subscribe to the idea that wizardry is required to use these tools. In fact, I barely know what I’m doing most of the time. I still get some stuff done.  
This is a work in progress. It probably gets some stuff wrong.  
  
– bpb / [p1k3](https://p1k3.com/) / [@brennen](https://twitter.com/brennen)

### [\#](https://p1k3.com/userland-book/#contents) contentsshow 

## [\#](https://p1k3.com/userland-book/#get-you-a-shell) 0. get you a shell 

You don’t have to have a shell at hand to get something out of this book. Still, as with most practical subjects, you’ll learn more if you try things out as you go. You shouldn’t feel guilty about skipping this section. It will always be here later if you need it.  
  
Not so long ago, it was common for schools and ISPs to hand out shell accounts on big shared systems. People learned the command line as a side effect of reading their e-mail.  
  
That doesn’t happen as often now, but in the meanwhile computers have become relatively cheap and free software is abundant. If you’re reading this on the web, you can probably get access to a shell. Some options follow.  


### [\#](https://p1k3.com/userland-book/#get-an-account-on-a-social-unix-server) get an account on a social unix server 

Check out [tilde.town](https://tilde.town/):  


> [tilde.town](http://tilde.town) is an intentional digital community for making art, socializing, and learning. Unlike many online spaces, users interact with [tilde.town](http://tilde.town) through a direct connection instead of a web site. This means using a tool called ssh and other text based tools.

### [\#](https://p1k3.com/userland-book/#use-a-raspberry-pi-or-beaglebone) use a raspberry pi or beaglebone 

Do you have a single-board computer laying around? Perfect. If you already run the standard Raspbian, Debian on a BeagleBone, or a similar-enough Linux, you don’t need much else. I wrote most of this text on a Raspberry Pi, and the example commands should all work there.  


### [\#](https://p1k3.com/userland-book/#use-a-virtual-machine) use a virtual machine 

A few options:  


* [Use Vagrant to spin up a machine in Virtualbox](https://docs.vagrantup.com/v2/getting-started/index.html) 
* [Use DigitalOcean to create a remotely-hosted VM running Linux](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server) 

## [\#](https://p1k3.com/userland-book/#the-command-line-as-literary-environment) 1. the command line as literary environment 

There’re a lot of ways to structure an introduction to the command line. I’m going to start with writing as a point of departure because, aside from web development, it’s what I use a computer for most. I want to shine a light on the humane potential of ideas that are usually understood as nerd trivia. Computers have utterly transformed the practice of writing within the space of my lifetime, but it seems to me that writers as a class miss out on many of the software tools and patterns taken as a given in more “technical” fields.  
  
Writing, particularly writing of any real scope or complexity, is very much a technical task. It makes demands, both physical and psychological, of its practitioners. As with woodworkers, graphic artists, and farmers, writers exhibit strong preferences in their tools, materials, and environment, and they do so because they’re engaged in a physically and cognitively challenging task.  
  
My thesis is that the modern Linux command line is a pretty good environment for working with English prose and prosody, and that maybe this will illuminate the ways it could be useful in your own work with a computer, whatever that work happens to be.  


### [\#](https://p1k3.com/userland-book/#terms-and-definitions) terms and definitions 

What software are we actually talking about when we say “the command line”?  
  
For the purposes of this discussion, we’re talking about an environment built on a very old paradigm called Unix.  
  
…except what classical Unix really looks like is this:  
  
The Unix-like environment we’re going to use isn’t very classical, really. It’s an operating system kernel called Linux, combined with a bunch of things written by other people \(people in the GNU and Debian projects, and many others\). Purists will tell you that this isn’t properly Unix at all. In strict historical terms they’re right, or at least a certain kind of right, but for the purposes of my cultural agenda I’m going to ignore them right now.  
![](data:image/jpeg;base64,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)  
This is what’s called a shell. There are many different shells, but they pretty much all operate on the same idea: You navigate a filesystem and run programs by typing commands. Commands can be combined in various ways to make programs of their own, and in fact the way you use the computer is often just to write little programs that invoke other programs, turtles-all-the-way-down style.  
  
The standard shell these days is something called Bash, so we’ll use Bash. It’s what you’ll most often see in the wild. Like most shells, Bash is ugly and stupid in more ways than it is possible to easily summarize. It’s also an incredibly powerful and expressive piece of software.  


### [\#](https://p1k3.com/userland-book/#twisty-little-passages) twisty little passages 

Have you ever played a text-based adventure game or MUD, of the kind that describes a setting and takes commands for movement and so on? Readers of a certain age and temperament might recognize the opening of Crowther & Woods' Adventure, the great-granddaddy of text adventure games:  
  


```text
YOU ARE STANDING AT THE END OF A ROAD BEFORE A SMALL BRICK BUILDING.
AROUND YOU IS A FOREST.  A SMALL STREAM FLOWS OUT OF THE BUILDING ANd
DOWN A GULLY.

> GO EAST

YOU ARE INSIDE A BUILDING, A WELL HOUSE FOR A LARGE SPRING.

THERE ARE SOME KEYS ON THE GROUND HERE.

THERE IS A SHINY BRASS LAMP NEARBY.

THERE IS FOOD HERE.

THERE IS A BOTTLE OF WATER HERE.
```

  
You can think of the shell as a kind of environment you inhabit, in much the way your character inhabits an adventure game. The difference is that instead of navigating around virtual rooms and hallways with commands like `LOOK` and `EAST`, you navigate between directories by typing commands like `ls` and `cd notes`:  
  


```text
$ ls
code  Downloads  notes  p1k3  photos  scraps  userland-book
$ cd notes
$ ls
notes.txt  sparkfun  TODO.txt
```

  
`ls` lists files. Some files are directories, which means they can contain other files, and you can step inside of them by typing `cd` \(for **c**hange **d**irectory\).  
  
In the Macintosh and Windows world, directories have been called “folders” for a long time now. This isn’t the worst metaphor for what’s going on, and it’s so pervasive by now that it’s not worth fighting about. It’s also not exactly a great metaphor, since computer filesystems aren’t built very much like the filing cabinets of yore. A directory acts a lot like a container of some sort, but it’s an infinitely expandable one which may contain nested sub-spaces much larger than itself. Directories are frequently like the TARDIS: Bigger on the inside.  


### [\#](https://p1k3.com/userland-book/#cat) cat 

When you’re in the shell, you have many tools at your disposal - programs that can be used on many different files, or chained together with other programs. They tend to have weird, cryptic names, but a lot of them do very simple things. Tasks that might be a menu item in a big program like Word, like counting the number of words in a document or finding a particular phrase, are often programs unto themselves. We’ll start with something even more basic than that.  
  
Suppose you have some files, and you’re curious what’s in them. For example, suppose you’ve got a list of authors you’re planning to reference, and you just want to check its contents real quick-like. This is where our friend `cat` comes in:  
  


```text
$ cat authors_sff
Ursula K. Le Guin
Jo Walton
Pat Cadigan
John Ronald Reuel Tolkien
Vanessa Veselka
James Tiptree, Jr.
John Brunner
```

  
“Why,” you might be asking, “is the command to dump out the contents of a file to a screen called `cat`? What do felines have to do with anything?”  
  
It turns out that `cat` is actually short for “catenate”, which is a long word basically meaning “stick things together”. In programming, we usually refer to sticking two bits of text together as “string concatenation”, probably because programmers like to feel like they’re being very precise about very simple actions.  
  
Suppose you wanted to see the contents of a set of author lists:  
  


```text
$ cat authors_sff authors_contemporary_fic authors_nat_hist
Ursula K. Le Guin
Jo Walton
Pat Cadigan
John Ronald Reuel Tolkien
Vanessa Veselka
James Tiptree, Jr.
John Brunner
Eden Robinson
Vanessa Veselka
Miriam Toews
Gwendolyn L. Waring
```

### [\#](https://p1k3.com/userland-book/#wildcards) wildcards 

We’re working with three filenames: `authors_sff`, `authors_contemporary_fic`, and `authors_nat_hist`. That’s an awful lot of typing every time we want to do something to all three files. Fortunately, our shell offers a shorthand for “all the files that start with `authors_`”:  
  


```text
$ cat authors_*
Eden Robinson
Vanessa Veselka
Miriam Toews
Gwendolyn L. Waring
Ursula K. Le Guin
Jo Walton
Pat Cadigan
John Ronald Reuel Tolkien
Vanessa Veselka
James Tiptree, Jr.
John Brunner
```

  
In Bash-land, `*` basically means “anything”, and is known in the vernacular, somewhat poetically, as a “wildcard”. You should always be careful with wildcards, especially if you’re doing anything destructive. They can and will surprise the unwary. Still, once you’re used to the idea, they will save you a lot of RSI.  


### [\#](https://p1k3.com/userland-book/#sort) sort 

There’s a problem here. Our author list is out of order, and thus confusing to reference. Fortunately, since one of the most basic things you can do to a list is to sort it, someone else has already solved this problem for us. Here’s a command that will give us some organization:  
  


```text
$ sort authors_*
Eden Robinson
Gwendolyn L. Waring
James Tiptree, Jr.
John Brunner
John Ronald Reuel Tolkien
Jo Walton
Miriam Toews
Pat Cadigan
Ursula K. Le Guin
Vanessa Veselka
Vanessa Veselka
```

  
Does it bother you that they aren’t sorted by last name? Me too. As a partial solution, we can ask `sort` to use the second “field” in each line as its sort **k**ey \(by default, sort treats whitespace as a division between fields\):  
  


```text
$ sort -k2 authors_*
John Brunner
Pat Cadigan
Ursula K. Le Guin
Gwendolyn L. Waring
Eden Robinson
John Ronald Reuel Tolkien
James Tiptree, Jr.
Miriam Toews
Vanessa Veselka
Vanessa Veselka
Jo Walton
```

  
That’s closer, right? It sorted on “Cadigan” and “Veselka” instead of “Pat” and “Vanessa”. \(Of course, it’s still far from perfect, because the second field in each line isn’t necessarily the person’s last name.\)  


### [\#](https://p1k3.com/userland-book/#options) options 

Above, when we wanted to ask `sort` to behave differently, we gave it what is known as an option. Most programs with command-line interfaces will allow their behavior to be changed by adding various options. Options usually \(but not always!\) look like `-o` or `--option`.  
  
For example, if we wanted to see just the unique lines, irrespective of case, for a file called colors:  
  


```text
$ cat colors
RED
blue
red
BLUE
Green
green
GREEN
```

  
We could write this:  
  


```text
$ sort -uf colors
blue
Green
RED
```

  
Here `-u` stands for **u**nique and `-f` stands for **f**old case, which means to treat upper- and lower-case letters as the same for comparison purposes. You’ll often see a group of short options following the `-` like this.  


### [\#](https://p1k3.com/userland-book/#uniq) uniq 

Did you notice how Vanessa Veselka shows up twice in our list of authors? That’s useful if we want to remember that she’s in more than one category, but it’s redundant if we’re just worried about membership in the overall set of authors. We can make sure our list doesn’t contain repeating lines by using `sort`, just like with that list of colors:  
  


```text
$ sort -u -k2 authors_*
John Brunner
Pat Cadigan
Ursula K. Le Guin
Gwendolyn L. Waring
Eden Robinson
John Ronald Reuel Tolkien
James Tiptree, Jr.
Miriam Toews
Vanessa Veselka
Jo Walton
```

  
But there’s another approach to this — `sort` is good at only displaying a line once, but suppose we wanted to see a count of how many different lists an author shows up on? `sort` doesn’t do that, but a command called `uniq` does, if you give it the option `-c` for **c**ount.  
  
`uniq` moves through the lines in its input, and if it sees a line more than once in sequence, it will only print that line once. If you have a bunch of files and you just want to see the unique lines across all of those files, you probably need to run them through `sort` first. How do you do that?  
  


```text
$ sort authors_* | uniq -c
      1 Eden Robinson
      1 Gwendolyn L. Waring
      1 James Tiptree, Jr.
      1 John Brunner
      1 John Ronald Reuel Tolkien
      1 Jo Walton
      1 Miriam Toews
      1 Pat Cadigan
      1 Ursula K. Le Guin
      2 Vanessa Veselka
```

### [\#](https://p1k3.com/userland-book/#standard-IO) standard IO 

The `|` is called a “pipe”. In the command above, it tells your shell that instead of printing the output of `sort authors_*` right to your terminal, it should send it to `uniq -c`.  
  
Pipes are some of the most important magic in the shell. When the people who built Unix in the first place give interviews about the stuff they remember from the early days, a lot of them reminisce about the invention of pipes and all of the new stuff it immediately made possible.  
  
Pipes help you control a thing called “standard IO”. In the world of the command line, programs take **i**nput and produce **o**utput. A pipe is a way to hook the output from one program to the input of another.  
  
Unlike a lot of the weirdly named things you’ll encounter in software, the metaphor here is obvious and makes pretty good sense. It even kind of looks like a physical pipe.  
  
What if, instead of sending the output of one program to the input of another, you’d like to store it in a file for later use?  
  
Check it out:  
  


```text
$ sort authors_* | uniq > ./all_authors
```

```text
$ cat all_authors
Eden Robinson
Gwendolyn L. Waring
James Tiptree, Jr.
John Brunner
John Ronald Reuel Tolkien
Jo Walton
Miriam Toews
Pat Cadigan
Ursula K. Le Guin
Vanessa Veselka
```

  
I like to think of the `>` as looking like a little funnel. It can be dangerous — you should always make sure that you’re not going to clobber an existing file you actually want to keep.  
  
If you want to tack more stuff on to the end of an existing file, you can use `>>` instead. To test that, let’s use `echo`, which prints out whatever string you give it on a line by itself:  
  


```text
$ echo 'hello' > hello_world
```

```text
$ echo 'world' >> hello_world
```

```text
$ cat hello_world
hello
world
```

  
You can also take a file and pull it directly back into the input of a given program, which is a bit like a funnel going the other direction:  
  


```text
$ nl < all_authors
     1  Eden Robinson
     2  Gwendolyn L. Waring
     3  James Tiptree, Jr.
     4  John Brunner
     5  John Ronald Reuel Tolkien
     6  Jo Walton
     7  Miriam Toews
     8  Pat Cadigan
     9  Ursula K. Le Guin
    10  Vanessa Veselka
```

  
`nl` is just a way to **n**umber **l**ines. This command accomplishes pretty much the same thing as `cat all_authors | nl`, or `nl all_authors`. You won’t see it used as often as `|` and `>`, since most utilities can read files on their own, but it can save you typing `cat` quite as often.  
  
We’ll use these features liberally from here on out.  


### [\#](https://p1k3.com/userland-book/#code-help-code-and-man-pages) `--help` and man pages 

You can change the behavior of most tools by giving them different options. This is all well and good if you already know what options are available, but what if you don’t?  
  
Often, you can ask the tool itself:  
  


```text
$ sort --help
Usage: sort [OPTION]... [FILE]...
  or:  sort [OPTION]... --files0-from=F
Write sorted concatenation of all FILE(s) to standard output.

Mandatory arguments to long options are mandatory for short options too.
Ordering options:

  -b, --ignore-leading-blanks  ignore leading blanks
  -d, --dictionary-order      consider only blanks and alphanumeric characters
  -f, --ignore-case           fold lower case to upper case characters
  -g, --general-numeric-sort  compare according to general numerical value
  -i, --ignore-nonprinting    consider only printable characters
  -M, --month-sort            compare (unknown) < 'JAN' < ... < 'DEC'
  -h, --human-numeric-sort    compare human readable numbers (e.g., 2K 1G)
  -n, --numeric-sort          compare according to string numerical value
  -R, --random-sort           sort by random hash of keys
      --random-source=FILE    get random bytes from FILE
  -r, --reverse               reverse the result of comparisons
```

  
…and so on. \(It goes on for a while in this vein.\)  
  
If that doesn’t work, or doesn’t provide enough info, the next thing to try is called a man page. \(“man” is short for “manual”. It’s sort of an unfortunate abbreviation.\)  
  


```text
$ man sort

SORT(1)                         User Commands                        SORT(1)



NAME
       sort - sort lines of text files

SYNOPSIS
       sort [OPTION]... [FILE]...
       sort [OPTION]... --files0-from=F

DESCRIPTION
       Write sorted concatenation of all FILE(s) to standard output.
```

  
…and so on. Manual pages vary in quality, and it can take a while to get used to reading them, but they’re very often the best place to look for help.  
  
If you’re not sure what program you want to use to solve a given problem, you might try searching all the man pages on the system for a keyword. `man` itself has an option to let you do this - `man -k keyword` - but most systems also have a shortcut called `apropos`, which I like to use because it’s easy to remember if you imagine yourself saying “apropos of \[some problem I have\]…”  
  


```text
$ apropos -s1 sort
apt-sortpkgs (1)     - Utility to sort package index files
bunzip2 (1)          - a block-sorting file compressor, v1.0.6
bzip2 (1)            - a block-sorting file compressor, v1.0.6
comm (1)             - compare two sorted files line by line
sort (1)             - sort lines of text files
tsort (1)            - perform topological sort
```

  
It’s useful to know that the manual represented by `man` has numbered sections for different kinds of manual pages. Most of what the average user needs to know about lives in section 1, “User Commands”, so you’ll often see the names of different tools written like `sort(1)` or `cat(1)`. This can be a good way to make it clear in writing that you’re talking about a specific piece of software rather than a verb or a small carnivorous mammal. \(I specified `-s1` for section 1 above just to cut down on clutter, though in practice I usually don’t bother.\)  
  
Like other literary traditions, Unix is littered with this sort of convention. This one just happens to date from a time when the manual was still a physical book.  


### [\#](https://p1k3.com/userland-book/#wc) wc 

`wc` stands for **w**ord **c**ount. It does about what you’d expect - it counts the number of words in its input.  
  


```text
$ wc index.md
  736  4117 24944 index.md
```

  
736 is the number of lines, 4117 the number of words, and 24944 the number of characters in the file I’m writing right now. I use this constantly. Most obviously, it’s a good way to get an idea of how much you’ve written. `wc` is the tool I used to track my progress the last time I tried National Novel Writing Month:  
  


```text
$ find ~/p1k3/archives/2010/11 -regextype egrep -regex '.*([0-9]+|index)' -type f | xargs wc -w | tail -1
 6585 total
```

```text
$ cowsay 'embarrassing.'
 _______________
< embarrassing. >
 ---------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

  
Anyway. The less obvious thing about `wc` is that you can use it to count the output of other commands. Want to know how many unique authors we have?  
  


```text
$ sort authors_* | uniq | wc -l
10
```

  
This kind of thing is trivial, but it comes in handy more often than you might think.  


### [\#](https://p1k3.com/userland-book/#head-tail-and-cut) head, tail, and cut 

Remember our old pal `cat`, which just splats everything it’s given back to standard output?  
  
Sometimes you’ve got a piece of output that’s more than you actually want to deal with at once. Maybe you just want to glance at the first few lines in a file:  
  


```text
$ head -3 colors
RED
blue
red
```

  
…or maybe you want to see the last thing in a list:  
  


```text
$ sort colors | uniq -i | tail -1
red
```

  
…or maybe you’re only interested in the first “field” in some list. You might use `cut` here, asking it to treat spaces as delimiters between fields and return only the first field for each line of its input:  
  


```text
$ cut -d' ' -f1 ./authors_*
Eden
Vanessa
Miriam
Gwendolyn
Ursula
Jo
Pat
John
Vanessa
James
John
```

  
Suppose we’re curious what the few most commonly occurring first names on our author list are? Here’s an approach, silly but effective, that combines a lot of what we’ve discussed so far and looks like plenty of one-liners I wind up writing in real life:  
  


```text
$ cut -d' ' -f1 ./authors_* | sort | uniq -ci | sort -n | tail -3
      1 Ursula
      2 John
      2 Vanessa
```

  
Let’s walk through this one step by step:  
  
First, we have `cut` extract the first field of each line in our author lists.  
  


```text
cut -d' ' -f1 ./authors_*
```

  
Then we sort these results  
  


```text
| sort
```

  
and pass them to `uniq`, asking it for a case-insensitive count of each repeated line  
  


```text
| uniq -ci
```

  
then sort again, numerically,  
  


```text
| sort -n
```

  
and finally, we chop off everything but the last three lines:  
  


```text
| tail -3
```

  
If you wanted to make sure to count an individual author’s first name only once, even if that author appears more than once in the files, you could instead do:  
  


```text
$ sort -u ./authors_* | cut -d' ' -f1 | uniq -ci | sort -n | tail -3
      1 Ursula
      1 Vanessa
      2 John
```

### [\#](https://p1k3.com/userland-book/#tab-separated-values) tab separated values 

Notice above how we had to tell `cut` that “fields” in `authors_*` are delimited by spaces? It turns out that if you don’t use `-d`, `cut` defaults to using tab characters for a delimiter.  
  
Tab characters are sort of weird little animals. You can’t usually see them directly — they’re like a space character that takes up more than one space when displayed. By convention, one tab is usually rendered as 8 spaces, but it’s up to the software that’s displaying the character what it wants to do.  
  
\(In fact, it’s more complicated than that: Tabs are often rendered as marking tab stops, which is a concept I remember from 7th grade typing classes, but haven’t actually thought about in my day-to-day life for nearly 20 years.\)  
  
Here’s a version of our `all_authors` that’s been rearranged so that the first field is the author’s last name, the second is their first name, the third is their middle name or initial \(if we know it\) and the fourth is any suffix. Fields are separated by a single tab character:  
  


```text
$ cat all_authors.tsv
Robinson    Eden
Waring  Gwendolyn   L.
Tiptree James       Jr.
Brunner John
Tolkien John    Ronald Reuel
Walton  Jo
Toews   Miriam
Cadigan Pat
Le Guin Ursula  K.
Veselka Vanessa
```

  
That looks kind of garbled, right? In order to make it a little more obvious what’s happening, let’s use `cat -T`, which displays tab characters as `^I`:  
  


```text
$ cat -T all_authors.tsv
Robinson^IEden
Waring^IGwendolyn^IL.
Tiptree^IJames^I^IJr.
Brunner^IJohn
Tolkien^IJohn^IRonald Reuel
Walton^IJo
Toews^IMiriam
Cadigan^IPat
Le Guin^IUrsula^IK.
Veselka^IVanessa
```

  
It looks odd when displayed because some names are at or nearly at 8 characters long. “Robinson”, at 8 characters, overshoots the first tab stop, so “Eden” gets indented further than other first names, and so on.  
  
Fortunately, in order to make this more human-readable, we can pass it through `expand`, which turns tabs into a given number of spaces \(8 by default\):  
  


```text
$ expand -t14 all_authors.tsv
Robinson      Eden
Waring        Gwendolyn     L.
Tiptree       James                       Jr.
Brunner       John
Tolkien       John          Ronald Reuel
Walton        Jo
Toews         Miriam
Cadigan       Pat
Le Guin       Ursula        K.
Veselka       Vanessa
```

  
Now it’s easy to sort by last name:  
  


```text
$ sort -k1 all_authors.tsv | expand -t14
Brunner       John
Cadigan       Pat
Le Guin       Ursula        K.
Robinson      Eden
Tiptree       James                       Jr.
Toews         Miriam
Tolkien       John          Ronald Reuel
Veselka       Vanessa
Walton        Jo
Waring        Gwendolyn     L.
```

  
Or just extract middle names and initials:  
  


```text
$ cut -f3 all_authors.tsv

L.


Ronald Reuel



K.
```

  
It probably won’t surprise you to learn that there’s a corresponding `paste` command, which takes two or more files and stitches them together with tab characters. Let’s extract a couple of things from our author list and put them back together in a different order:  
  


```text
$ cut -f1 all_authors.tsv > lastnames
```

```text
$ cut -f2 all_authors.tsv > firstnames
```

```text
$ paste firstnames lastnames | sort -k2 | expand -t12
John        Brunner
Pat         Cadigan
Ursula      Le Guin
Eden        Robinson
James       Tiptree
Miriam      Toews
John        Tolkien
Vanessa     Veselka
Jo          Walton
Gwendolyn   Waring
```

  
As these examples show, TSV is something very like a primitive spreadsheet: A way to represent information in columns and rows. In fact, it’s a close cousin of CSV, which is often used as a lowest-common-denominator format for transferring spreadsheets, and which represents data something like this:  
  


```text
last,first,middle,suffix
Tolkien,John,Ronald Reuel,
Tiptree,James,,Jr.
```

  
The advantage of tabs is that they’re supported by a bunch of the standard tools. A disadvantage is that they’re kind of ugly and can be weird to deal with, but they’re useful anyway, and character-delimited rows are often a good-enough way to hack your way through problems that call for basic structure.  


### [\#](https://p1k3.com/userland-book/#finding-text-grep) finding text: grep 

After all those contortions, what if you actually just want to see which lists an individual author appears on?  
  


```text
$ grep 'Vanessa' ./authors_*
./authors_contemporary_fic:Vanessa Veselka
./authors_sff:Vanessa Veselka
```

  
`grep` takes a string to search for and, optionally, a list of files to search in. If you don’t specify files, it’ll look through standard input instead:  
  


```text
$ cat ./authors_* | grep 'Vanessa'
Vanessa Veselka
Vanessa Veselka
```

  
Most of the time, piping the output of `cat` to `grep` is considered silly, because `grep` knows how to find things in files on its own. Many thousands of words have been written on this topic by leading lights of the nerd community.  
  
You’ve probably noticed that this result doesn’t contain filenames \(and thus isn’t very useful to us\). That’s because all `grep` saw was the lines in the files, not the names of the files themselves.  


### [\#](https://p1k3.com/userland-book/#now-you-have-n-problems) now you have n problems 

To close out this introductory chapter, let’s spend a little time on a topic that will likely vex, confound, and \(occasionally\) delight you for as long as you are acquainted with the command line.  
  
When I was talking about `grep` a moment ago, I fudged the details more than a little by saying that it expects a string to search for. What `grep` actually expects is a pattern. Moreover, it expects a specific kind of pattern, what’s known as a regular expression, a cumbersome phrase frequently shortened to regex.  
  
There’s a lot of theory about what makes up a regular expression. Fortunately, very little of it matters to the short version that will let you get useful stuff done. The short version is that a regex is like using wildcards in the shell to match groups of files, but for text in general and with more magic.  
  


```text
$ grep 'Jo.*' ./authors_*
./authors_sff:Jo Walton
./authors_sff:John Ronald Reuel Tolkien
./authors_sff:John Brunner
```

  
The pattern `Jo.*` says that we’re looking for lines which contain a literal `Jo`, followed by any quantity \(including none\) of any character. In a regex, `.` means “anything” and `*` means “any amount of the preceding thing”.  
  
`.` and `*` are magical. In the particular dialect of regexen understood by `grep`, other magical things include:  


| `^`  | start of a line  |
| :--- | :--- |
| `$`  | end of a line  |
| `[abc]`  | one of a, b, or c  |
| `[a-z]`  | a character in the range a through z  |
| `[0-9]`  | a character in the range 0 through 9  |
| `+`  | one or more of the preceding thing  |
| `?`  | 0 or 1 of the preceding thing  |
| `*`  | any number of the preceding thing  |
| `(foo|bar)`  | "foo" or "bar"  |
| `(foo)?`  | optional "foo"  |

  
It’s actually a little more complicated than that: By default, if you want to use a lot of the magical characters, you have to prefix them with `\`. This is both ugly and confusing, so unless you’re writing a very simple pattern, it’s often easiest to call `grep -E`, for **E**xtended regular expressions, which means that lots of characters will have special meanings.  
  
Authors with 4-letter first names:  
  


```text
$ grep -iE '^[a-z]{4} ' ./authors_*
./authors_contemporary_fic:Eden Robinson
./authors_sff:John Ronald Reuel Tolkien
./authors_sff:John Brunner
```

  
A count of authors named John:  
  


```text
$ grep -c '^John ' ./all_authors
2
```

  
Lines in this file matching the words “magic” or “magical”:  
  


```text
$ grep -iE 'magic(al)?' ./index.md
Pipes are some of the most important magic in the shell.  When the people who
shell to match groups of files, but with more magic.
`.` and `*` are magical.  In the particular dialect of regexen understood
by `grep`, other magical things include:
use a lot of the magical characters, you have to prefix them with `\`.  This is
Lines in this file matching the words "magic" or "magical":
    $ grep -iE 'magic(al)?' ./index.md
```

  
Find some “-agic” words in a big list of words:  
  


```text
$ grep -iE '(m|tr|pel)agic' /usr/share/dict/words
magic
magic's
magical
magically
magician
magician's
magicians
pelagic
tragic
tragically
tragicomedies
tragicomedy
tragicomedy's
```

  
`grep` isn’t the only - or even the most important - tool that makes use of regular expressions, but it’s a good place to start because it’s one of the fundamental building blocks for so many other operations. Filtering lists of things, matching patterns within collections, and writing concise descriptions of how text should be transformed are at the heart of a practical approach to Unix-like systems. Regexen turn out to be a seductively powerful way to do these things - so much so that they’ve crept their way into text editors, databases, and full-featured programming languages.  
  
There’s a dark side to all of this, for the truth about regular expressions is that they are ugly, inconsistent, brittle, and incredibly difficult to think clearly about. They take years to master and reward the wielder with great power, but they are also a trap: a temptation towards the path of cleverness masquerading as wisdom.  
  
✑  
  
I’ll be returning to this theme, but for the time being let’s move on. Now that we’ve established, however haphazardly, some of the basics, let’s consider their application to a real-world task.  
  


## [\#](https://p1k3.com/userland-book/#a-literary-problem) 2. a literary problem 

The [previous chapter](https://p1k3.com/literary_environment) introduced a bunch of tools using contrived examples. Now we’ll look at a real problem, and work through a solution by building on tools we’ve already covered.  
  
So on to the problem: I write poetry.  
{rimshot dot wav}  
  
Most of the poems I have written are not very good, but lately I’ve been thinking that I’d like to comb through the last ten years' worth and pull the least-embarrassing stuff into a single collection.  
  
I’ve hinted at how the contents of my blog are stored as files, but let’s take a look at the whole thing:  
  


```text
$ ls -F ~/p1k3/archives/
1997/  2003/  2009/  bones/     meta/
1998/  2004/  2010/  chapbook/  winfield/
1999/  2005/  2011/  cli/       wip/
2000/  2006/  2012/  colophon/
2001/  2007/  2013/  europe/
2002/  2008/  2014/  hack/
```

  
\(`ls`, again, just lists files. `-F` tells it to append a character that shows it what type of file we’re looking at, such as a trailing / for directories. `~` is a shorthand that means “my home directory”, which in this case is `/home/brennen`.\)  
  
Each of the directories here holds other directories. The ones for each year have sub-directories for the months of the year, which in turn contain files for the days. The files are just little pieces of HTML and Markdown and some other stuff. Many years ago, before I had much of an idea how to program, I wrote a script to glue them all together into a web page and serve them up to visitors. This all sounds complicated, but all it really means is that if I want to write a blog entry, I just open a file and type some stuff. Here’s an example for March 1st:  
  


```text
$ cat ~/p1k3/archives/2014/3/1
<h1>Saturday, March 1</h1>

<markdown>
Sometimes I'm going along on a Saturday morning, still a little dazed from the
night before, and I think something like "I should just go write a detailed
analysis of hooded sweatshirts".  Mostly these thoughts don't survive contact
with an actual keyboard.  It's almost certainly for the best.
</markdown>
```

  
And here’s an older one that contains a short poem:  
  


```text
$ cat ~/p1k3/archives/2012/10/9
<h1>tuesday, october 9</h1>

<freeverse>i am a stateful machine
i exist in a manifold of consequence
a clattering miscellany of impure functions
and side effects</freeverse>
```

  
Notice that `<freeverse>` bit? It kind of looks like an HTML tag, but it’s not. What it actually does is tell my blog script that it should format the text it contains like a poem. The specifics don’t matter for our purposes \(yet\), but this convention is going to come in handy, because the first thing I want to do is get a list of all the entries that contain poems.  
  
Remember `grep`?  
  


```text
$ grep -ri '<freeverse>' ~/p1k3/archives > ~/possible_poems
```

  
Let’s step through this bit by bit:  
  
First, I’m asking `grep` to search **r**ecursively, **i**gnoring case. “Recursively” just means that every time the program finds a directory, it should descend into that directory and search in any files there as well.  
  


```text
grep -ri
```

  
Next comes a pattern to search for. It’s in single quotes because the characters `<` and `>` have a special meaning to the shell, and here we need the shell to understand that it should treat them as literal angle brackets instead.  
  


```text
'<freeverse>'
```

  
This is the path I want to search:  
  


```text
~/p1k3/archives
```

  
Finally, because there are so many entries to search, I know the process will be slow and produce a large list, so I tell the shell to redirect it to a file called `possible_poems` in my home directory:  
  


```text
> ~/possible_poems
```

  
This is quite a few instances…  
  


```text
$ wc -l ~/possible_poems
679 /home/brennen/possible_poems
```

  
…and it’s also not super-pretty to look at:  
  


```text
$ head -5 ~/possible_poems
/home/brennen/p1k3/archives/2011/10/14:<freeverse>i've got this friend has a real knack
/home/brennen/p1k3/archives/2011/4/25:<freeverse>i can't claim to strive for it
/home/brennen/p1k3/archives/2011/8/10:<freeverse>one diminishes or becomes greater
/home/brennen/p1k3/archives/2011/8/12:<freeverse>
/home/brennen/p1k3/archives/2011/1/1:<freeverse>six years on
```

  
Still, it’s a decent start. I can see paths to the files I have to check, and usually a first line. Since I use a fancy text editor, I can just go down the list opening each file in a new window and copying the stuff I’m interested in to a new file.  
  
This is good enough for government work, but what if instead of jumping around between hundreds of files, I’d rather read everything in one file and just weed out the bad ones as I go?  
  


```text
$ cat `grep -ril '<freeverse>' ~/p1k3/archives` > ~/possible_poems_full
```

  
This probably bears some explaining. `grep` is still doing all the real work here. The main difference from before is that `-l` tells grep to just list any files it finds which contain a match.  
  


```text
`grep -ril '<freeverse>' ~/p1k3/archives`
```

  
Notice those backticks around the grep command? This part is a little trippier. It turns out that if you put backticks around something in a command, it’ll get executed and replaced with its result, which in turn gets executed as part of the larger command. So what we’re really saying is something like:  
  


```text
$ cat [all of the files in the blog directory with <freeverse> in them]
```

  
Did you catch that? I just wrote a command that rewrote itself as a different, more specific command. And it appears to have worked on the first try:  
  


```text
$ wc ~/possible_poems_full
 17628  80980 528699 /home/brennen/possible_poems_full
```

  
Welcome to wizard school.  


## [\#](https://p1k3.com/userland-book/#programmerthink) 3. programmerthink 

In the [preceding chapter](https://p1k3.com/userland-book/#a-literary-problem), I worked through accumulating a big piece of text from some other, smaller texts. I started with a bunch of files and wound up with one big file called `potential_poems_full`.  
  
Let’s talk for a minute about how programmers approach problems like this one. What I’ve just done is sort of an old-school humanities take on things: Metaphorically speaking, I took a book off the shelf and hauled it down to the copy machine to xerox a bunch of pages, and now I’m going to start in on them with a highlighter and some Post-Its or something. A process like this will often trigger a cascade of questions in the programmer-mind:  


* What if, halfway through the project, I realize my selection criteria were all wrong and have to backtrack? 
* What if I discover corrections that also need to be made in the source documents? 
* What if I want to access metadata, like the original location of a file? 
* What if I want to quickly re-order the poems according to some new criteria? 
* Why am I storing the same text in two different places? 

A unifying theme of these questions is that they could all be answered by involving a little more abstraction.  
  
★  
  
Some kinds of abstraction are so common in the physical world that we can forget they’re part of a sophisticated technology. For example, a good deal of bicycle maintenance can be accomplished with a cheap multi-tool containing a few different sizes of hex wrench and a couple of screwdrivers.  
  
A hex wrench or screwdriver doesn’t really know anything about bicycles. All it really knows about is fitting into a space and allowing torque to be applied. Standardized fasteners and adjustment mechanisms on a bicycle ensure that the work can be done anywhere, by anyone with a certain set of tools. Standard tools mean that if you can work on a particular bike, you can work on most bikes, and even on things that aren’t bikes at all, but were designed by people with the same abstractions in mind.  
  
The relationship between a wrench, a bolt, and the purpose of a bolt is a lot like something we call indirection in software. Programs like `grep` or `cat` don’t really know anything about poetry. All they really know about is finding lines of text in input, or sticking inputs together. Files, lines, and text are like standardized fasteners that allow a user who can work on one kind of data \(be it poetry, a list of authors, the source code of a program\) to use the same tools for other problems and other data.  
  
★  
  
When I first started writing stuff on the web, I edited a page — a single HTML file — by hand. When the entries on my nascent blog got old, I manually cut-and-pasted them to archive files with names like `old_main97.html`, which held all of the stuff I’d written in 1997.  
  
I’m not holding this up as an example of youthful folly. In fact, it worked fine, and just having a single, static file that you can open in any text editor has turned out to be a lot more future-proof than the sophisticated blogging software people were starting to write at the time.  
  
And yet. Something about this habit nagged at my developing programmer mind after a few years. It was just a little bit too manual and repetitive, a little bit silly to have to write things like a table of contents by hand, or move entries around by copy-and-pasting them to different files. Since I knew the date for each entry, and wanted to make them navigable on that basis, why not define a directory structure for the years and months, and then write a file to hold each day? That way, all I’d have to do is concatenate the files in one directory to display any given month:  
  


```text
$ cat ~/p1k3/archives/2014/1/* | head -10
<h1>Sunday, January 12</h1>

<h2>the one casey is waiting for</h2>

<freeverse>
after a while
the thing about drinking
is that it just feeds
what you drink to kill
and kills
```

  
I ultimately wound up writing a few thousand lines of Perl to do the actual work, but the essential idea of the thing is still little more than invoking `cat` on some stuff.  
  
I didn’t know the word for it at the time, but what I was reaching for was a kind of indirection. By putting blog posts in a specific directory layout, I was creating a simple model of the temporal structure that I considered their most important property. Now, if I want to write commands that ask questions about my blog posts or re-combine them in certain ways, I can address my concerns to this model. Maybe, for example, I want a rough idea how many words I’ve written in blog posts so far in 2014:  
  


```text
$ find ~/p1k3/archives/2014/ -type f | xargs cat | wc -w
6677
```

  
`xargs` is not the most intuitive command, but it’s useful and common enough to explain here. At the end of last chapter, when I said:  
  


```text
$ cat `grep -ril '<freeverse>' ~/p1k3/archives` > ~/possible_poems_full
```

  
I could also have written this as:  
  


```text
$ grep -ril '<freeverse>' ~/p1k3/archives | xargs cat > ~/possible_poems_full
```

  
What this does is take its input, which starts like:  
  


```text
/home/brennen/p1k3/archives/2002/10/16
/home/brennen/p1k3/archives/2002/10/27
/home/brennen/p1k3/archives/2002/10/10
```

  
…and run `cat` on all the things in it:  
  


```text
cat /home/brennen/p1k3/archives/2002/10/16 /home/brennen/p1k3/archives/2002/10/27 /home/brennen/p1k3/archives/2002/10/10 ...
```

  
It can be a better idea to use `xargs`, because while backticks are incredibly useful, they have some limitations. If you’re dealing with a very large list of files, for example, you might exceed the maximum allowed length for arguments to a command on your system. `xargs` is smart enough to know that limit and run `cat` more than once if needed.  
  
`xargs` is actually sort of a pain to think about, and will make you jump through some irritating hoops if you have spaces or other weirdness in your filenames, but I wind up using it quite a bit.  
  
Maybe I want to see a table of contents:  
  


```text
$ find ~/p1k3/archives/2014/ -type d | xargs ls -v | head -10
/home/brennen/p1k3/archives/2014/:
1
2
3
4

/home/brennen/p1k3/archives/2014/1:
5
12
14
```

  
Or find the subtitles I used in 2013:  
  


```text
$ find ~/p1k3/archives/2012/ -type f | xargs perl -ne 'print "$1\n" if m{<h2>(.*?)</h2>}'
pursuit
fragment
this poem again
i'll do better next time
timebinding animals
more observations on gear nerdery &amp; utility fetishism
thrift
A miracle, in fact, means work
<em>technical notes for late october</em>, or <em>it gets dork out earlier these days</em>
radio
light enough to travel
12:06am
"figures like Heinlein and Gingrich"
```

  
The crucial thing about this is that the filesystem itself is just like `cat` and `grep`: It doesn’t know anything about blogs \(or poetry\), and it’s basically indifferent to the actual structure of a file like `~/p1k3/archives/2014/1/12`. What the filesystem knows is that there are files with certain names in certain places. It need not know anything about the meaning of those names in order to be useful; in fact, it’s best if it stays agnostic about the question, for this enables us to assign our own meaning to a structure and manipulate that structure with standard tools.  
  
★  
  
Back to the problem at hand: I have this collection of files, and I know how to extract the ones that contain poems. My goal is to see all the poems and collect the subset of them that I still find worthwhile. Just knowing how to grep and then edit a big file solves my problem, in a basic sort of way. And yet: Something about this nags at my mind. I find that, just as I can already use standard tools and the filesystem to ask questions about all of my blog posts in a given year or month, I would like to be able to ask questions about the set of interesting poems.  
  
If I want the freedom to execute many different sorts of commands against this set of poems, it begins to seem that I need a model.  
  
When programmers talk about models, they often mean something that people in the sciences would recognize: We find ways to represent the arrangement of facts so that we can think about them. A structured representation of things often means that we can change those things, or at least derive new understanding of them.  
  
★  
  
At this point in the narrative, I could pretend that my next step is immediately obvious, but in fact it’s not. I spend a couple of days thinking off and on about how to proceed, scribbling notes during bus rides and while drinking beers at the pizza joint down the street. I assess and discard ideas which fall into a handful of broad approaches:  


* Store blog entries in a relational database system which would allow me to associate them with data like “this entry is in a collection called ‘ok poems’”. 
* Selectively build up a file containing the list of files with ok poems, and use it to do other tasks. 
* Define a format for metadata that lives within entry files. 
* Turn each interesting file into a directory of its own which contains a file with the original text and another file with metadata. 

I discard the relational database idea immediately: I like working with files, and I don’t feel like abandoning a model that’s served me well for my entire adult life.  
  
Building up an index file to point at the other files I’m working with has a certain appeal. I’m already most of the way there with the `grep` output in `potential_poems`. It would be easy to write shell commands to add, remove, sort, and search entries. Still, it doesn’t feel like a very satisfying solution unto itself. I’d like to know that an entry is part of the collection just by looking at the entry, without having to cross-reference it to a list somewhere else.  
  
What about putting some meaningful text in the file itself? I thought about a bunch of different ways to do this, some of them really complicated, and eventually arrived at this:  
  


```text
<!-- collection: ok-poems -->
```

  
The `<!-- -->` bits are how you define a comment in HTML, which means that neither my blog code nor web browsers nor my text editor have to know anything about the format, but I can easily find files with certain values. Check it:  
  


```text
$ find ~/p1k3/archives -type f | xargs perl -ne 'print "$ARGV[0]: $1 -> $2\n" if m{<!-- ([a-z]+): (.*?) -->};'
/home/brennen/p1k3/archives/2014/2/9: collection -> ok-poems
```

  
That’s an ugly one-liner, and I haven’t explained half of what it does, but the comment format actually seems pretty workable for this. It’s a little tacky to look at, but it’s simple and searchable.  
  
Before we settle, though, let’s turn to the notion of making each entry into a directory that can contain some structured metadata in a separate file. Imagine something like:  
  


```text
$ ls ~/p1k3/archives/2013/2/9
index  Meta
```

  
Here I use the name “index” for the main part of the entry because it’s a convention of web sites for the top-level page in a directory to be called something like `index.html`. As it happens, my blog software already supports this kind of file layout for entries which contain multiple parts, image files, and so forth.  
  


```text
$ head ~/p1k3/archives/2013/2/9/index
<h1>saturday, february 9</h1>

<freeverse>
midwinter midafternoon; depressed as hell
sitting in a huge cabin in the rich-people mountains
writing a sprawl, pages, of melancholic midlife bullshit

outside the snow gives way to broken clouds and the
clear unyielding light of the high country sun fills

$ cat ~/p1k3/archives/2013/2/9/Meta
collection: ok-poems
```

  
It would then be easy to `find` files called `Meta` and grep them for `collection: ok-poems`.  
  
What if I put metadata right in the filename itself, and dispense with the grep altogether?  
  


```text
$ ls ~/p1k3/archives/2013/2/9
index  meta-ok-poem

$ find ~/p1k3/archives -name 'meta-ok-poem'
/home/brennen/archives/2013/2/9/meta-ok-poem
```

  
There’s a lot to like about this. For one thing, it’s immediately visible in a directory listing. For another, it doesn’t require searching through thousands of lines of text to extract a specific string. If a directory has a `meta-ok-poem` in it, I can be pretty sure that it will contain an interesting `index`.  
  
What are the downsides? Well, it requires transforming lots of text files into directories-containing-files. I might automate that process, but it’s still a little tedious and it makes the layout of the entry archive more complicated overall. There’s a cost to doing things this way. It lets me extend my existing model of a blog entry to include arbitrary metadata, but it also adds steps to writing or finding blog entries.  
  
Abstractions usually cost you something. Is this one worth the hassle? Sometimes the best way to answer that question is to start writing code that handles a given abstraction.  
  


## [\#](https://p1k3.com/userland-book/#script) 4. script 

Back in chapter 1, I said that “the way you use the computer is often just to write little programs that invoke other programs”. In fact, we’ve already gone over a bunch of these. Grepping through the text of a previous chapter should pull up some good examples:  
  


```text
$ grep -E '\$ [a-z]+.*\| ' ../literary_environment/index.md
    $ sort authors_* | uniq -c
    $ sort authors_* | uniq > ./all_authors
    $ find ~/p1k3/archives/2010/11 -regextype egrep -regex '.*([0-9]+|index)' -type f | xargs wc -w | tail -1
    $ sort authors_* | uniq | wc -l
    $ sort colors | uniq -i | tail -1
    $ cut -d' ' -f1 ./authors_* | sort | uniq -ci | sort -n | tail -3
    $ sort -u ./authors_* | cut -d' ' -f1 | uniq -ci | sort -n | tail -3
    $ sort -k1 all_authors.tsv | expand -t14
    $ paste firstnames lastnames | sort -k2 | expand -t12
    $ cat ./authors_* | grep 'Vanessa'
```

  
None of these one-liners do all that much, but they all take input of one sort or another and apply one or more transformations to it. They’re little formal sentences describing how to make one thing into another, which is as good a definition of programming as most. Or at least this is a good way to describe programming-in-the-small. \(A lot of the programs we use day-to-day are more like essays, novels, or interminable Fantasy series where every character you like dies horribly than they are like individual sentences.\)  
  
One-liners like these are all well and good when you’re staring at a terminal, trying to figure something out - but what about when you’ve already figured it out and you want to repeat it in the future?  
  
It turns out that Bash has you covered. Since shell commands are just text, they can live in a text file as easily as they can be typed.  


### [\#](https://p1k3.com/userland-book/#learn-you-an-editor) learn you an editor 

We’ve skirted the topic so far, but now that we’re talking about writing out text files in earnest, you’re going to want a text editor.  
  
My editor is where I spend most of my time that isn’t in a web browser, because it’s where I write both code and prose. It turns out that the features which make a good code editor overlap a lot with the ones that make a good editor of English sentences.  
  
So what should you use? Well, there have been other contenders in recent years, but in truth nothing comes close to dethroning the Great Old Ones of text editing. Emacs is a creature both primal and sophisticated, like an avatar of some interstellar civilization that evolved long before multicellular life existed on earth and seeded the galaxy with incomprehensible artefacts and colossal engineering projects. Vim is like a lovable chainsaw-studded robot with the most elegant keyboard interface in history secretly emblazoned on its shining diamond heart.  
  
It’s worth the time it takes to learn one of the serious editors, but there are easier places to start. Nano, for example, is easy to pick up, and should be available on most systems. To start it, just say:  
  


```text
$ nano file
```

  
You should see something like this:  
![](data:text/xml;base64,/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCACUAQADASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDT07x78KovC9lbSNpyX6WkSSF9KcneFAbLeUec5559eaq2fjn4eRTqbm90aSE4yo0iTK/PkgfueflGOcdT6c+WfEHwZY+Erfw9JZ3FxMdSsFupfOKnaxA4XAHHPeuJoA+kL3x/8OWkkNldaIqM6lRLor/KvORxDz2/KrFn8QfhdHPN9qn0iWHGItujOG9s/uRz69foMc/M9FAH0f8A8J98NTphh36OLksCJBp0pC5JyM+Rk4GOvU56CrI+IHwsbVUnaTSVtBGVMI0mQndk8/6kdRt+mD1618z0UAfU/wDwsb4Of9Q3/wAE7/8Axuj/AIWN8HP+ob/4J3/+N18sUUAfU/8Awsb4Of8AUN/8E7//ABuj/hY3wc/6hv8A4J3/APjdfLFFAH1P/wALG+Dn/UN/8E7/APxuj/hY3wc/6hv/AIJ3/wDjdfLFFAH0fqnjz4cSXYk0y90aKIhQyTaK5wRuyR+675H/AHyOnd8nj/4aSaVNEZ9EF4ZB5bpo8qrsBHX91nJAPT1r5tooA+il8bfDee3Zbq/0tJRDJGjQaS4BYhQrH9z1GG+mauW3j/4Xreubi60lrUMxRE0V9xHGAxMX1z7/AJV800UAfU//AAsb4Of9Q3/wTv8A/G6P+FjfBz/qG/8Agnf/AON18sUUAfU//Cxvg5/1Df8AwTv/APG6P+FjfBz/AKhv/gnf/wCN18sUUAfU/wDwsb4Of9Q3/wAE7/8Axuj/AIWN8HP+ob/4J3/+N18sUUAfU/8Awsb4Of8AUN/8E7//ABuj/hY3wc/6hv8A4J3/APjdfLFFAH1P/wALG+Dn/UN/8E7/APxuj/hY3wc/6hv/AIJ3/wDjdfLFFAH1P/wsb4Of9Q3/AME7/wDxuj/hY3wc/wCob/4J3/8AjdfLFFAH1P8A8LG+Dn/UN/8ABO//AMbo/wCFjfBz/qG/+Cd//jdfLFFAH1P/AMLG+Dn/AFDf/BO//wAbqhrfxA+ElzoOowWf9n/apLWVIdukup3lSFwfL45xzXzPRQBJLcTzhBNNJIEG1d7E7R6DPSo6KKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiig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)  
Arrow keys will move your cursor around, and typing stuff will make it appear in the file. This is pretty much like every other editor you’ve ever used. If you haven’t used Nano before, that stuff along the bottom of the terminal is a reference to the most commonly used commands. `^` is a convention for “Ctrl”, so `^O` means Ctrl-o \(the case of the letter doesn’t actually matter\), which will save the file you’re working on. Ctrl-x will quit, which is probably the first important thing to know about any given editor.  


### [\#](https://p1k3.com/userland-book/#d-i-y-utilities) d.i.y. utilities 

So back to putting commands in text files. Here’s a file I just created in my editor:  
  


```text
$ cat okpoems
#!/bin/bash

# find all the marker files and get the name of
# the directory containing each
find ~/p1k3/archives -name 'meta-ok-poem' | xargs -n1 dirname

exit 0
```

  
This is known as a script. There are a handful of things to notice here. First, there’s this fragment:  
  


```text
#!/bin/bash
```

  
The `#!` right at the beginning, followed by the path to a program, is a special sequence that lets the kernel know what program should be used to interpret the contents of the file. `/bin/bash` is the path on the filesystem where Bash itself lives. You might see this referred to as a shebang or a hash bang.  
  
Lines that start with a `#` are comments, used to describe the code to a human reader. The `exit 0` tells Bash that the currently running script should exit with a status of 0, which basically means “nothing went wrong”.  
  
If you examine the directory listing for `okpoems`, you’ll see something important:  
  


```text
$ ls -l okpoems
-rwxrwxr-x 1 brennen brennen 163 Apr 19 00:08 okpoems
```

  
That looks pretty cryptic. For the moment, just remember that those little `x`s in the first bit mean that the file has been marked e**x**ecutable. We accomplish this by saying something like:  
  


```text
$ chmod +x ./okpoems
```

  
Once that’s done, it and the shebang line in combination mean that typing `./okpoems` will have the same effect as typing `bash okpoems`:  
  


```text
$ ./okpoems
/home/brennen/p1k3/archives/2013/2/9
/home/brennen/p1k3/archives/2012/3/17
/home/brennen/p1k3/archives/2012/3/26
```

### [\#](https://p1k3.com/userland-book/#heavy-lifting) heavy lifting 

`okpoems` demonstrates the basics, but it doesn’t do very much. Here’s a script with a little more substance to it:  
  


```text
$ cat markpoem
#!/bin/bash

# $1 is the first parameter to our script
POEM=$1

# Complain and exit if we weren't given a path:
if [ ! $POEM ]; then
  echo 'usage: markpoem <path>'

  # Confusingly, an exit status of 0 means to the shell that everything went
  # fine, while any other number means that something went wrong.
  exit 64
fi

if [ ! -e $POEM ]; then
  echo "$POEM not found"
  exit 66
fi

echo "marking $POEM an ok poem"

POEM_BASENAME=$(basename $POEM)

# If the target is a plain file instead of a directory, make it into
# a directory and move the content into $POEM/index:
if [ -f $POEM ]; then
  echo "making $POEM into a directory, moving content to"
  echo "  $POEM/index"
  TEMPFILE="/tmp/$POEM_BASENAME.$(date +%s.%N)"
  mv $POEM $TEMPFILE
  mkdir $POEM
  mv $TEMPFILE $POEM/index
fi

if [ -d $POEM ]; then
  # touch(1) will either create the file or update its timestamp:
  touch $POEM/meta-ok-poem
else
  echo "something broke - why isn't $POEM a directory?"
  file $POEM
fi

# Signal that all is copacetic:
echo kthxbai
exit 0
```

  
Both of these scripts are imperfect, but they were quick to write, they’re made out of standard commands, and I don’t yet hate myself for them: All signs that I’m not totally on the wrong track with the `meta-ok-poem` abstraction, and could live with it as part of an ongoing writing project. `okpoems` and `markpoem` would also be easy to use with custom keybindings in my editor. In a few more lines of code, I can build a system to wade through the list of candidate files and quickly mark the interesting ones.  


### [\#](https://p1k3.com/userland-book/#generality) generality 

So what’s lacking here? Well, probably a bunch of things, feature-wise. I can imagine writing a script to unmark a poem, for example. That said, there’s one really glaring problem. “Ok poem” is only one kind of property a blog entry might possess. Suppose I wanted a way to express that a poem is terrible?  
  
It turns out I already know how to add properties to an entry. If I generalize just a little, the tools become much more flexible.  
  


```text
$ ./addprop /home/brennen/p1k3/archives/2012/3/26 meta-terrible-poem
marking /home/brennen/p1k3/archives/2012/3/26 with meta-terrible-poem
kthxbai
```

```text
$ ./findprop meta-terrible-poem
/home/brennen/p1k3/archives/2012/3/26
```

  
`addprop` is only a little different from `markpoem`. It takes two parameters instead of one - the target entry and a property to add.  
  


```text
$ cat addprop
#!/bin/bash

ENTRY=$1
PROPERTY=$2

# Complain and exit if we weren't given a path and a property:
if [[ ! $ENTRY || ! $PROPERTY ]]; then
  echo "usage: addprop <path> <property>"
  exit 64
fi

if [ ! -e $ENTRY ]; then
  echo "$ENTRY not found"
  exit 66
fi

echo "marking $ENTRY with $PROPERTY"

# If the target is a plain file instead of a directory, make it into
# a directory and move the content into $ENTRY/index:
if [ -f $ENTRY ]; then
  echo "making $ENTRY into a directory, moving content to"
  echo "  $ENTRY/index"

  # Get a safe temporary file:
  TEMPFILE=`mktemp`

  mv $ENTRY $TEMPFILE
  mkdir $ENTRY
  mv $TEMPFILE $ENTRY/index
fi

if [ -d $ENTRY ]; then
  touch $ENTRY/$PROPERTY
else
  echo "something broke - why isn't $ENTRY a directory?"
  file $ENTRY
fi

echo kthxbai
exit 0
```

  
Meanwhile, `findprop` is more or less `okpoems`, but with a parameter for the property to find:  
  


```text
$ cat findprop
#!/bin/bash

if [ ! $1 ]
then
  echo "usage: findprop <property>"
  exit
fi

# find all the marker files and get the name of
# the directory containing each
find ~/p1k3/archives -name $1 | xargs -n1 dirname

exit 0
```

  
These scripts aren’t much more complicated than their poem-specific counterparts, but now they can be used to solve problems I haven’t even thought of yet, and included in other scripts that need their functionality.  
  


## [\#](https://p1k3.com/userland-book/#general-purpose-programmering) 5. general purpose programmering 

I didn’t set out to write a book about programming, as such, but because programming and the command line are so inextricably linked, this text draws near the subject almost of its own accord.  
  
If you’re not terribly interested in programming, this chapter can easily enough be skipped. It’s more in the way of philosophical rambling than concrete instruction, and will be of most use to those with an existing background in writing code.  
  
✢  
  
If you’ve used computers for more than a few years, you’re probably viscerally aware that most software is fragile and most systems decay. In the time since I took my first tentative steps into the little world of a computer \(a friend’s dad’s unidentifiable gaming machine, my own father’s blue monochrome Zenith laptop, the Apple II\) the churn has been overwhelming. By now I’ve learned my way around vastly more software — operating systems, programming languages and development environments, games, editors, chat clients, mail systems — than I presently could use if I wanted to. Most of it has gone the way of some ancient civilization, surviving \(if at all\) only in faint, half-understood cultural echoes and occasional museum-piece displays. Every user of technology becomes, in time, a refugee from an irretrievably recent past.  
  
And yet, despite all this, the shell endures. Most of the ideas in this book are older than I am. Most of them could have been applied in 1994 or thereabouts, when I first logged on to multiuser systems running AT&T Unix. Since the early 1990s, systems built on a fundamental substrate of Unix-like behavior and abstractions have proliferated wildly, becoming foundational at once to the modern web, the ecosystem of free and open software, and the technological dominance ca. 2014 of companies like Apple, Google, and Facebook.  
  
Why is this, exactly?  
  
✣  
  
As I’ve said \(and hopefully shown\), the commands you write in your shell are essentially little programs. Like other programs, they can be stored for later use and recombined with other commands, creating new uses for your ideas.  
  
It would be hard to say that there’s any one reason command line environments remain so vital after decades of evolution and hard-won refinement in computer interfaces, but it seems like this combinatory nature is somewhere near the heart of it. The command line often lacks the polish of other interfaces we depend on, but in exchange it offers a richness and freedom of expression rarely seen elsewhere, and invites its users to build upon its basic facilities.  
  
What is it that makes last chapter’s `addprop` preferable to the more specific `markpoem`? Let’s look at an alternative implementation of `markpoem`:  
  


```text
$ cat simple_markpoem
#!/bin/bash

addprop $1 meta-ok-poem
```

  
Is this script trivial? Absolutely. It’s so trivial that it barely seems to exist, because I already wrote `addprop` to do all the heavy lifting and play well with others, freeing us to imagine new uses for its central idea without worrying about the implementation details.  
  
Unlike `markpoem`, `addprop` doesn’t know anything about poetry. All it knows about, in fact, is putting a file \(or three\) in a particular place. And this is in keeping with a basic insight of Unix: Pieces of software that do one very simple thing generalize well. Good command line tools are like a hex wrench, a hammer, a utility knife: They embody knowledge of turning, of striking, of cutting — and with this kind of knowledge at hand, the user can change the world even though no individual tool is made with complete knowledge of the world as a whole. There’s a lot of power in the accumulation of small competencies.  
  
Of course, if your code is only good at one thing, to be of any use, it has to talk to code that’s good at other things. There’s another basic insight in the Unix tradition: Tools should be composable. All those little programs have to share some assumptions, have to speak some kind of trade language, in order to combine usefully. Which is how we’ve arrived at standard IO, pipelines, filesystems, and text as as a lowest-common-denominator medium of exchange. If you think about most of these things, they have some very rough edges, but they give otherwise simple tools ways to communicate without becoming super-complicated along the way.  
  
✤  
  
What is the command line?  
The command line is an environment of tool use.  
So are kitchens, workshops, libraries, and programming languages.  
  
✥  
  
Here’s a confession: I don’t like writing shell scripts very much, and I can’t blame anyone else for feeling the same way.  
  
That doesn’t mean you shouldn’t know about them, or that you shouldn’t write them. I write little ones all the time, and the ability to puzzle through other people’s scripts comes in handy. Oftentimes, the best, most tasteful way to automate something is to build a script out of the commonly available commands. The standard tools are already there on millions of machines. Many of them have been pretty well understood for a generation, and most will probably be around for a generation or three to come. They do neat stuff. Scripts let you build on ideas you’ve already worked out, and give repeatable operations a memorable, user-friendly name. They encourage reuse of existing programs, and help express your ideas to people who’ll come after you.  
  
One of the reliable markers of powerful software is that it can be scripted: It extends to its users some of the same power that its authors used in creating it. Scriptable software is to some extent living software. It’s a book that you, the reader, get to help write.  
  
In all these ways, shell scripts are wonderful, a little bit magical, and quietly indispensable to the machinery of modern civilization.  
  
Unfortunately, in all the ways that a shell like Bash is weird, finicky, and covered in 40 years of incidental cruft, long-form Bash scripts are even worse. Bash is a useful glue language, particularly if you’re already comfortable wiring commands together. Syntactic and conceptual innovations like pipes are beautiful and necessary. What Bash is not, despite its power, is a very good general purpose programming language. It’s just not especially good at things like math, or complex data structures, or not looking like a punctuation-heavy variety of alphabet soup.  
  
It turns out that there’s a threshold of complexity beyond which life becomes easier if you switch from shell scripting to a more robust language. Just where this threshold is located varies a lot between users and problems, but I often think about switching languages before a script gets bigger than I can view on my screen all at once. `addprop` is a good example:  
  


```text
$ wc -l ../script/addprop
41 ../script/addprop
```

  
41 lines is a touch over what fits on one screen in the editor I usually use. If I were going to add much in the way of features, I’d think pretty hard about porting it to another language first.  
  
What’s cool is that if you know a language like C, Python, Perl, Ruby, PHP, or JavaScript, your code can participate in the shell environment as a first class citizen simply by respecting the conventions of standard IO, files, and command line arguments. Often, in order to create a useful utility, it’s only necessary to deal with `STDIN`, or operate on a particular sort of file, and most languages offer simple conventions for doing these things.  
  
\*  
  
I think the shell can be taught and understood as a humane environment, despite all of its ugliness and complication, because it offers the materials of its own construction to its users, whatever their concerns. The writer, the philosopher, the scientist, the programmer: Files and text and pipes know little enough about these things, but in their very indifference to the specifics of any one complex purpose, they’re adaptable to the basic needs of many. Simple utilities which enact simple kinds of knowledge survive and recombine because there is a wisdom to be found in small things.  
  
Files and text know nothing about poetry, nothing in particular of the human soul. Neither do pen and ink, printing presses or codex books, but somehow we got Shakespeare and Montaigne.  
  


## [\#](https://p1k3.com/userland-book/#one-of-these-things-is-not-like-the-others) 6. one of these things is not like the others 

If you’re the sort of person who took a few detours into the history of religion in college, you might be familiar with some of the ways people used to do textual comparison. When pen, paper, and typesetting were what scholars had to work with, they did some fairly sophisticated things in order to expose the relationships between multiple pieces of text.  
![](data:text/xml;base64,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)  
Here’s a book I got in college: Gospel Parallels: A Comparison of the Synoptic Gospels, Burton H. Throckmorton, Jr., Ed. It breaks up three books from the New Testament by the stories and themes that they contain, and shows the overlapping sections of each book that contain parallel texts. You can work your way through and see what parts only show up in one book, or in two but not the other, or in all three. Pages are arranged like so:  
  


```text
                 § JESUS DOES SOME STUFF
     ________________________________________________
    |  MAT            |    MAR             |  LUK    |
    |-----------------+--------------------+---------|
    | Stuff           |                    |         |
    |                 | Stuff              |         |
    |                 | Stuff              | Stuff   |
    |                 | Stuff              |         |
    |                 | Stuff              |         |
    |                 |                    |         |
```

  
The way I understand it, a book like this one only scratches the surface of the field. Tools like this support a lot of theory about which books copied each other and how, and what other sources they might have copied that we’ve since lost.  
  
This is some incredibly dry material, even if you kind of dig thinking about the questions it addresses. It takes a special temperament to actually sit poring over fragmentary texts in ancient languages and do these painstaking comparisons. Even if you’re a writer or editor and work with a lot of revisions of a text, there’s a good chance you rarely do this kind of comparison on your own work, because that shit is tedious.  


### [\#](https://p1k3.com/userland-book/#diff) diff 

It turns out that academics aren’t the only people who need tools for comparing different versions of a text. Working programmers, in fact, need to do this constantly. Programmers are also happiest when putting off the actual task at hand to solve some incidental problem that cropped up along the way, so by now there are a lot of ways to say “here’s how this file is different from this file”, or “here’s how this file is different from itself a year ago”.  
q  
Let’s look at a couple of shell scripts from an earlier chapter:  
  


```text
$ cat ../script/okpoems
#!/bin/bash

# find all the marker files and get the name of
# the directory containing each
find ~/p1k3/archives -name 'meta-ok-poem' | xargs -n1 dirname

exit 0
```

```text
$ cat ../script/findprop
#!/bin/bash

if [ ! $1 ]
then
  echo "usage: findprop <property>"
  exit
fi

# find all the marker files and get the name of
# the directory containing each
find ~/p1k3/archives -name $1 | xargs -n1 dirname

exit 0
```

  
It’s pretty obvious these are similar files, but do we know what exactly changed between them at a glance? It wouldn’t be hard to figure out, once. If you wanted to be really certain about it, you could print them out, set them side by side, and go over them with a highlighter.  
  
  
Now imagine doing that for a bunch of files, some of them hundreds or thousands of lines long. I’ve actually done that before, colored markers and all, but I didn’t feel smart while I was doing it. This is a job for software.  


```text
$ diff ../script/okpoems ../script/findprop
2a3,8
> if [ ! $1 ]
> then
>   echo "usage: findprop <property>"
>   exit
> fi
> 
5c11
< find ~/p1k3/archives -name 'meta-ok-poem' | xargs -n1 dirname
---
> find ~/p1k3/archives -name $1 | xargs -n1 dirname
```

  
That’s not the most human-friendly output, but it’s a little simpler than it seems at first glance. It’s basically just a way of describing the changes needed to turn `okpoems` into `findprop`. The string `2a3,8` can be read as “at line 2, add lines 3 through 8”. Lines with a `>` in front of them are added. `5c11` can be read as “line 5 in the original file becomes line 11 in the new file”, and the `<` line is replaced with the `>` line. If you wanted, you could take a copy of the original file and apply these instructions by hand in your text editor, and you’d wind up with the new file.  
  
A lot of people \(me included\) prefer what’s known as a “unified” diff, because it’s easier to read and offers context for the changed lines. We can ask for one of these with `diff -u`:

```text
$ diff -u ../script/okpoems ../script/findprop
--- ../script/okpoems   2014-04-19 00:08:03.321230818 -0600
+++ ../script/findprop  2014-04-21 21:51:29.360846449 -0600
@@ -1,7 +1,13 @@
 #!/bin/bash

+if [ ! $1 ]
+then
+  echo "usage: findprop <property>"
+  exit
+fi
+
 # find all the marker files and get the name of
 # the directory containing each
-find ~/p1k3/archives -name 'meta-ok-poem' | xargs -n1 dirname
+find ~/p1k3/archives -name $1 | xargs -n1 dirname

 exit 0
```

  
That’s a little longer, and has some metadata we might not always care about, but if you look for lines starting with `+` and `-`, it’s easy to read as “added these, took away these”. This diff tells us at a glance that we added some lines to complain if we didn’t get a command line argument, and replaced `'meta-ok-poem'` in the `find` command with that argument. Since it shows us some context, we have a pretty good idea where those lines are in the file and what they’re for.  
  
What if we don’t care exactly how the files differ, but only whether they do?

```text
$ diff -q ../script/okpoems ../script/findprop
Files ../script/okpoems and ../script/findprop differ
```

  
I use `diff` a lot in the course of my day job, because I spend a lot of time needing to know just how two programs differ. Just as importantly, I often need to know how \(or whether!\) the output of programs differs. As a concrete example, I want to make sure that `findprop meta-ok-poem` is really a suitable replacement for `okpoems`. Since I expect their output to be identical, I can do this:

```text
$ ../script/okpoems > okpoem_output
```

```text
$ ../script/findprop meta-ok-poem > findprop_output
```

```text
$ diff -s okpoem_output findprop_output
Files okpoem_output and findprop_output are identical
```

  
The `-s` just means that `diff` should explicitly tell us if files are the **s**ame. Otherwise, it’d output nothing at all, because there aren’t any differences.  
  
As with many other tools, `diff` doesn’t very much care whether it’s looking at shell scripts or a list of filenames or what-have-you. If you read the man page, you’ll find some features geared towards people writing C-like programming languages, but its real specialty is just text files with lines made out of characters, which works well for lots of code, but certainly could be applied to English prose.  
  
Since I have a couple of versions ready to hand, let’s apply this to a text with some well-known variations and a bit of a literary legacy. Here’s the first day of the Genesis creation narrative in a couple of English translations:  


