---
layout: post
title: "Emacs: Down The Rabbit Hole"
date: 2014-10-30 06:05:25 -0400
comments: true
categories: [emacs, editors, coding]
---

So I wrote [Welcome to The Dark Side: Switching to Emacs](http://decomplecting.org/blog/2014/10/23/welcome-to-the-dark-side-switching-to-emacs/) in response to a tweet, but as any of my co-workers will attest, it doesn't take much to get me started on my Emacs workflow.

I feel like a religious convert... I miss those simple, unadorned Vim services but I'm floored by the majesty of the stained glass and altar dressings and ritual of the Church of Emacs.

So before the jump, in the spirit of "I'll show you mine if you show me yours," my [.emacs.d](https://github.com/canweriotnow/.emacs.d).

## An Unexpected Journey

I lived in my happy little Vim hobbit hole, smoking my pipe and enjoying my brandy. It was not a dirty hole, or a sandy hole, but a hobbit hole, which means comfort.

One day, a wizard visted me.

{% img /images/post-img/mccarthy1.jpg 'McCarthy at work at SAIL' %}

And that's when things began to get weird...

<!-- more -->

Okay, so maybe I didn't receive a visit from the revenant spirit of John McCarthy, ghost of programming past, present and future. Or maybe I did.

Maybe Paul Graham just convinced me I was [coding in Blub](http://www.paulgraham.com/avg.html), for whatever value of Blub I happened to be using.

See, the thing about Blub is it's a mutable value. When you're using C++ and Java comes along, you realize C++ was actually Blub. When you're using Perl for your day-to-day and discover Python, and then Ruby, you realize that not only was Python Blub, but Perl was an even Blubbier Blub.

Ruby... oh, Ruby. I still love Ruby. But then something happened.

I need to backpedal a bit.

There's _using_ a language, and then there's _building_ something in it. I'd played with Scheme ([SICP](http://mitpress.mit.edu/sicp/) is wonderful), and even Common Lisp, and I knew enough to appreciate the Lisp-nature of Ruby which, when combined with its Smalltalk-nature, I thought made for hte perfect productive language.

But see, I was _building_ things in Ruby while I was _playing_ with Lisp.

Along comes Clojure.

I was working in a pretty isolated programming role that granted me a lot of de facto autonomy. So when I got a request for a new service, I thought "why not Clojure?"

We're in late 2012 here, so bear with me.

My first Clojure project ran like a champ, was hailed as an unqualified success. Eventually I even [blogged about](http://decomplecting.org/blog/2013/02/03/datetime-conversions-in-clojure/) a piece of that project that handled datetimes.

Fast-forward to the present, I've written Clojure in [Sublime Text](http://www.sublimetext.com/), [Atom](https://atom.io/), mostly [Vim](http://www.vim.org/) with the help of some awesome plugins from [Tim Pope](https://github.com/tpope).

Like I [mentioned before](http://decomplecting.org/blog/2014/10/23/welcome-to-the-dark-side-switching-to-emacs/), I've had a religious hatred for Emacs since the mid-1990s when I entered the *nix world and got involved in USENET.

<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/freebsdgirl">@freebsdgirl</a> <a href="https://twitter.com/darkuncle">@darkuncle</a> ...and on that day, war broke out, destroying the fragile peace that had been brokered so long ago.</p>&mdash; jason λewis (@canweriotnow) <a href="https://twitter.com/canweriotnow/status/527532324234489857">October 29, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

The war is far from over...

...but, I digress.

I started the [Baltimore Clojure Meetup](http://www.meetup.com/Baltimore-Clojure/) and met more Emacs users than I had in one place in a long time. Again, I dismissed Emacs.

That is, until I found [LightTable](http://lighttable.com/) completely b0rked again and threw up my hands.

Perhaps I shouldn't have eaten my hands to begin with... sorry, equivocation humor. Can't resist.

## Welcome to Emacs

So yeah, I went over my starter packages in the [earlier post](http://decomplecting.org/blog/2014/10/23/welcome-to-the-dark-side-switching-to-emacs/), but I didn't talk about the full experience of discovery I underwent when I fully committed to emacs.

Sure, there's the whole `cider-mode` and `cider-jack-in` and `cider-nrepl` and even `cider-scratch` that make LightTable's inline evaluation modes look like child's play (no offense to Chris Granger, LightTable is beautiful, I love it, but... y'know, Emacs).

So I did those things, started with [Prelude](http://batsov.com/prelude/), added all the Clojure fun I could find, and got to work.

I also subscribed to [/r/emacs](http://www.reddit.com/r/emacs), and did a little reading on the [Emacs Wiki](http://www.emacswiki.org/emacs/).

Have you ever been comfortably reading (or coding) under a tree, and you see a white rabbit in a waistcoat with a pocket-watch run by complaining he's late?

Thus such adventures begin.

## EAT ME / DRINK ME

As I fell to the bottom (or so I thought) of the rabbit-hole, I found a bottle of `cider` labeled _Drink Me,_ and so I drank the `cider`. Suddenly, I could eval Clojure inline, jump to docstrings, jump to source for a fn, and it was wonderful.

The last time I tried Emacs, I always joked about how I was using Emacs but always edited my .emacs config with Vim.

"Not this time," I thought, and used [Projectile](http://www.emacswiki.org/emacs/Projectile) to manage my `.emacs.d` and edited my `user.el` in Emacs. Oh, it was better! Then, thought I, I should put my `.emacs.d` in source control (actually, it was demanded:

<blockquote class="twitter-tweet" data-conversation="none" lang="en"><p><a href="https://twitter.com/canweriotnow">@canweriotnow</a> <a href="https://twitter.com/willowdower">@willowdower</a> Now you must post your config on github so that we may critique it.</p>&mdash; Alex Redington (@holy_chao) <a href="https://twitter.com/holy_chao/status/511574770388041728">September 15, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

...yeah).

But then I realized I was doing the `⌘-Tab` to iTerm to run `git ci -a` (I pity the fool that doesn't alias common git commoands) in... wait for it... `$EDITOR=/usr/bin/vim`.

That's when I found a bit of fairy cake called [magit](http://www.emacswiki.org/Magit), and I ate a bit of that and my Git workflow was inside of Emacs. Now it was a simple `M-x magit-status` to view my working tree state, where I could hit `s` to stage files for commit, and `C-c C-c` to commit changes, and `P P` to push.

Oh, it's beautiful.

## Curiouser and Curiouser

Well, if Emacs can handle my Git workflow, what _can't_ it do, I wondered?

I went a bit mad playing with multiple buffer and frame layouts; on one occasion I opened a shell inside an emacs biffer and launched the command-line version of emacs in a shell inside the windowed version of emacs.

Recursive rabbit holes.

When you're running the Cocoa-nested version of Emacs (not Aquamacs, fuck that noise, but just GNU Emacs packaged as a .app), you get some suggestions from the menus. Gnus for USENET or email, various games, a calendar...

Calendar?

That's whan I discovered Org-Mode.

## Org-Mode FTW

[Org Mode](http://orgmode.org/) is an Emacs major mode that lets you organize your life. All of it. I'm not even going into detail here, it's a deep, deep well. You can use it for a TODO list, sync it with your phone, use it [to write](http://www.railsonmaui.com/blog/2014/03/05/octopress-setup-with-github-and-org-mode-v2/) your [Octopress blog](http://octopress.org).

(Confession: This blog is powered by octopress, and although it's now written in Emacs, I've not gone full crazy and started composing it with Org-Mode)

## Twittering-Mode WTF

That's when I started going down the tunnel of "well, what _else_ can it do?"

And I discovered `twittering-mode`.

A quick `M-x package-install RET twittering-mode` puts a Twitter client in your text editor. Like you always needed. `M-x twit` will jump you right into your Twitter feed, `i` will enable user icons (yes, user avatars right in goddamn Emacs), and `u` will jump you to a buffer where you can compose a Tweet and hit `C-c C-c` to send it.

## Playing Games

I'd be remiss if I didn't mention that `M-x package-install RET 2048-mode` will install a game of 2048 in Emacs. Because that's really fucking important, you know?

**Sigh**

For good reason, Emacs comes standard with an AI psychotherapist named Eliza.

A quick `M-x doctor` and you're in therapy.

Which you'll probably need.

## ...and Much, Much More

I've barely scratched the surface, but I feel like this post is long enough. There's so much down here, down the Emacs rabbit hole, that it will probably take me weeks to even catch up to whre I am right now; what I've described so far is my first few days with this ~~operating system~~ text editor.

But it's a fun ride.

### Postscript

Sorry for the Tolkien digression when my dominant allusion was _Alice in Wonderland..._ Emacs is a weird place.
