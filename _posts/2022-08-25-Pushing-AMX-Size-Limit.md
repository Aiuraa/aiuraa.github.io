---
layout: post
title: "Pushing AMX Size Limit"
categories: development
---

# Pushing AMX Size Limit
Yesterday i made some little experiment based on my friend posts about having ~200 MB AMX size in a single Megabytes of code, originally i'm only explaining to him on how this size works and why should you care to the code, but i only get around ~11 to ~24 MB size of AMX which you can see below:

![Me having 11 MB AMX Size](/assets/img/2022-08-25/first-size.png)

This is just normal since my initial code, i'm only using a library called "YSI-Includes" especially on "y\_iterator/y\_foreach" which it will allocate whatever the size you put into the iterator, for example: `new Iterator: myIter<ITER_SIZE>;`. 

Let's just assume `ITER_SIZE` is `1000` placed in two or three seperate array which array is a byte so if i'm not wrong, the calculation should be like this `(1000 * 4) * 2` or `* 3` which can cause huge amount of megabytes but it's still be considered as ___Normal Size___ compared to what i'm about to share with you.

When i was sharing my code into a discord channel, A guy named Alex is Y\_Less came to me and give some really good piece of code on "How to make your AMX size go 1 GB" which makes me wonder "If it possible?, i mean so far i only witnessed 200 MB size and never saw beyond that number" and so i was thinking that he's joking but seeing how great he was in the community makes me want to challenge myself to trying reach 1 GB with any means and so the journey begins.

First, i went to make the code worst by using he's first code he gave me with 2d array which it looks like this:

```c
#define JUNK_SIZE 10_000
new junk_function[JUNK_SIZE][JUNK_SIZE];

```

This, with calculation that array will always multiplied by four `(size * 4)`, combined with another (`size * 4`) will give the results what i'm expected and thus i began to reach +100 MB first try. Then i try to add the second code he gave me about involving with `switch case` jump. As you can see, pawn `switch case` is really weird according to him and also have different behaviour compared to other languages `switch case` and that's why always using `if` and `else` might be better option than `switch case` if the checks you want to do is still _possible_ to do it with `if` and `else`.

The code itself looks like this:

```c
new unused[JUNK_SIZE];
switch (unused[0])
{
    case 0..100000: { print("Hello World"); } 
}

```

The code itself looks innocent enough but if you look closer, it's not because the worst part is in the `unused` variable and the `case 0..100000` code which will make your AMX Binary Size go brrrr (having more than 100 MB size). Editing any of that code sizes will result in "Full Disk" error which the compiler cannot actually hold almost all of the binary code that is converted from Pawn, and so the final result is about ~700 MB (actually it's 172 MB capped) and it took 3 or 5 minutes to actually compiles it with Linux.

![Look mom, i did it](/assets/img/2022-08-25/final-size.png)

You can actually try and build the code yourself by clicking [This link](https://github.com/Aiuraa/test-pawn-size) if you're curious if the code can actually compiles to 700 MB, the instructions and other things are also provided in the repo.

Since unfortunately i cannot make the binary beyond ~700 MB due to "allegedly" having the size capped (32 bit integer limit), i cannot do anything about it and thus ending my journey to getting the most huge size i've ever done and also teaching people about they should really care about their code or else it will look like that code where a few kilobytes of codes can give you __HUGE__ sizes due to worst code that you've been putting. 
