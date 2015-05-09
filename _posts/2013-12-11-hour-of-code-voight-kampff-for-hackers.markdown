---
layout: post
title: "Hour of Code: Voight-Kampff for Hackers?"
date: 2013-12-11 20:20
comments: true
categories: [csedweek, code.org, coding]
---

So, [Gizmodo](http://gizmodo.com) has a great post on the new series of [Code.org](http://code.org) PSAs, ["People Who Did Not Get Rich and/or Famous Coding Want You to Code"](http://gizmodo.com/people-who-did-not-get-rich-and-or-famous-coding-want-y-1479863703). I think [Computer Science Education Week](http://csedweek.org/) is a fantastic idea (although IMHO every week should be CSEdWeek), but the whole "hour of code" thing seemed slightly silly, until now.

Okay, the PSAs keep it silly. Every time someone in those videos says "I just did _n_ lines of code", the following script runs through my head:

{% codeblock lang:ruby "Yeah, this..." %}
"I just did #{n} lines of code".gsub!(/code/, 'coke') << ", and I can't feel my face!"
{% endcodeblock %}

Yeah, I'm a terrible person. Also hilarious. Moving on...

<!-- more -->

### Hacker Exceptionalism

Usually, the term [Exceptionalism](http://en.wikipedia.org/wiki/Exceptionalism) is used in a context of superiority, e.g., [American exceptionalism](http://en.wikipedia.org/wiki/American_exceptionalism). I do believe there is something like "hacker exceptionalism", except the "exception" has nothing to do with superiority, but literally an exceptional case — a corner case for life, if you will.

There's something weird about hackers. I'm not lumping everyone who writes code for their day job into this category (frankly, that would be offensive to my sensibilities). I've written [before](http://decomplecting.org/blog/2012/05/22/passion/) about my encounters with people who just code 9 to 5 and then don't think about it and all I can say now is that I wish they would stop (actually, I'm not sure many of them think about it at all).

People who grok code have weird brains. That's the theory. It's not new; in [_Snow Crash_](http://www.nealstephenson.com/snowcrash/), Neal Stephenson describes a neurolinguistic virus that can infect the brains of hackers via digital images because of the pathways coding has created in their brains.

There's a chicken-and-egg problem here: are our brains weird because we're hackers, or are we hackers because our brains are weird?

I'm not sure there's any way to answer that scientifically until we have longitudinal studies complete with periodic fMRI scans of children as they develop into programmers (or not). So we'll leave the origin story aside for now.

### Voight-Kampff

In the movie [_Blade Runner_](http://en.wikipedia.org/wiki/Blade_Runner) (apologies to Philip K. Dick fans for heading down this particular rabbit-hole), a test called [Voight-Kampff](http://bladerunner.wikia.com/wiki/Voight-Kampff_machine) is administered to distinguish humans from replicants.

The idea of a Voight-Kampff test to distinguish humans from hackers isn't new either; in 2006, researchers proposed an (apparently) effective test to separate [programming sheep from non-programming goats](http://www.codinghorror.com/blog/2006/07/separating-programming-sheep-from-non-programming-goats.html).

{% pullquote %}
So this "Hour of Code" thing. I thought it was a cute idea at first, became dubious, got annoyed at the marketing, and stopped paying attention until the new batch of PSAs were covered on Gizmodo (full confession: I was reading [Valleywag](http://valleywag.gawker.com/) when I saw it. I can't help myself). {"Then I realized: this is like a Voight-Kampff test for hackers."} My first "hour of code" was when I was five. that hour stretched into three. Then countless hours followed. For the rest of my life.
{% endpullquote %}

The whole "everyone should learn to code" meme is great; I think everyone should understand the fundamentals of computer science. Not that "learning to code" is equivalent to "understanding CS fundamentals," but it's a step in the right direction. But it's important to distinguish between "learning to code" and "entering a career in software engineering."

I wish the latter were left to true hackers. The ones who are outed by the "hour of code" when the hour turns into 10,000 hours; the ones who go from "I did 5 lines of code!" to "I did 5k LOCs" in about two weeks. That's not going to be everyone. It's going to be a distinct minority. We're corner cases.

Code.org has some great goals, even if the motives seem questionable at times (does it feel to anyone else like "everyone should learn to code" is in some cases an attempt to rekindle the failed 1990's experiment of "commodity programmers"?). More than anything else, though, "hour of code" seems to intorduce a `catch` block for those of us who throw `HackerBrainException`. And that's great. Uncaught exceptions aren't good for anyone. This is why we need [computing in the core](http://www.computinginthecore.org/) — it's like checked exceptions in the API for public education.

### Computer Science in K-12

This is the real issue, isn't it? Getting computer science into the standards for K-12 education? Making an "hour of code" redundant?

Sadly, things don't seem to have changed much since my own [negative experiences with coding at school](http://decomplecting.org/blog/2013/06/02/were-not-ready-to-teach-kids-to-code/)... but that was in the late 1990's. I would have expected progress since then... if I were a lot more naïve.

So a message to current students: **Fortuna audaces iuvat** — Fortune favors the bold. Hack everything. Code your math homework. Shit, code your math homework, put hte source on [Github](https://github.com), and let your friends *copy* that shit. Refuse to do anything without a computer, whether that computer is your phone or a [Cray XE6](http://www.cray.com/Products/Computing/XE.aspx).

If your school doesn't offer CS classes, start your own. [Just get hacking](http://decomplecting.org/blog/2013/11/12/just-get-hacking/). If you throw `HackerBrainException`, you'll never stop.
