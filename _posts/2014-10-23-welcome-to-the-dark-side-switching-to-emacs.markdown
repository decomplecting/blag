---
layout: post
title: "Welcome to The Dark Side: Switching to Emacs"
date: 2014-10-23 20:42:40 -0400
comments: true
categories: [coding, Clojure, emacs, editors]
---

I have to start this post by saying I've been a dogmatic [Vim](http://www.vim.org/) partisan since the 1990's, when I started using vi on the Solaris and Irix boxen I had access to, and then on my own machines when I got started with Linux in 1994.

I flamed against Emacs on Usenet, called it all the epithets (Escape Meta Alt Ctrl Delete, Eight Megs And Constantly Swapping (8 megs was a lot then), Eventually Mangles All Computer Storage)... I couldn't stand the chord keys and lack of modality.

Even once I got heavily into Lisp I still tried to stick with Vim, or tried LightTable, or Atom, or SublimeText. But then one day I hit a wall and Emacs (plus cider-mode and slime and a few other packages) was the obvious solution. Now I'm out there evangelizing Emacs (I'm writing this post in the Markdown major mode plus some helpful minor modes) and I figure I'd offer some advice for those looking to convert to the Church of Emacs.

![St. Ignucius](/images/post-img/ignucius.png)

<!--more-->

Primarily, this post is inspired by a request I received on Twitter:

<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/canweriotnow">@canweriotnow</a> Got any links for switching to emacs? macvim isn&#39;t working in yosemite so I figure I might as well give emacs a real shot</p>&mdash; maɪk pətɛlə (@mikepatella) <a href="https://twitter.com/mikepatella/status/525439599276220416">October 24, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Instead of just compiling some links in a gist, I figured it was worthy of a blog post, so my seniors in the Church of Emacs can tell me where I'm wrong in the comments. But this is based on my experience converting from Vim to Emacs, so I'll explain what worked for me.

### Emacs Prelude

Prelude is really a great way to hit the ground running. It provides a wealth of sensible default packages, fixes the color scheme, and configures your `.emacs.d` config directory in a way that makes it easy to configure without breaking shit.

The install instructions are [here](http://batsov.com/prelude/) and I highly recommend it.

**UPDATE:** I forgot something vitally important about prelude. Prelude comes with `guru-mode` enabled by default, which disables your arrow keys and prods you to use Emacs default navigation commands instead (i.e. `C-p` for up, `C-n` for down, `C-b` for left, `C-f` for right). These commands are [worth knowing](https://www.gnu.org/software/emacs/manual/html_node/emacs/Moving-Point.html), but I felt like I was being trolled when my arrow keys just told me what chord combination to use instead. (As an aside, [Thoughtbot's](http://thoughtbot.com) [dotfiles](https://github.com/thoughtbot/dotfiles) do the same thing with vim).

So you have two options: one is to `M-x guru-mode` to toggle it every session. The more permanent solution is to add the following to your config (if you're using Prelude, it should go in `~/.emacs.d/personal/preload/user.el`):

`(setq prelude-guru nil)`

Just my personal preference, but something I found really annoying when I got started.

As far as all those useful navigation and editing commands, emacs (naturally) has a built-in tutorial accessible from `M-x help-with-tutorial` or just `C-h t`.

**UPDATE TO THE UPDATE:**

Bozhidar Batsov (the author of Prelude) pointed out in [this comment](http://decomplecting.org/blog/2014/10/23/welcome-to-the-dark-side-switching-to-emacs/#comment-1651596560) that the current default behavior is to warn when arrow keys are used, not to disable them.

I hadn't noticed the change, which came in with [this commit](https://github.com/bbatsov/prelude/commit/fda768992ef27f39f30178d4ebb8cbb559d5a3c6).

You can find the configuration options for `guru-mode` in the README [here](https://github.com/bbatsov/prelude#warnings-on-arrow-navigation-in-editor-buffers).


### Emacs for Mac OS X

I really like using the packaged app version of Emacs available from [http://emacsformacosx.com/](http://emacsformacosx.com/). It works great with Prelude, and doesn't include the cruft that [Aquamacs](http://aquamacs.org/) tacks on to make it more Mac-ish.

You get a nice packaged Emacs.app that follows OS X conventions, but is really just straight GNU Emacs.

### evil-mode

So, this is a touchy subject for me. When I first switched I used evil-mode to get my familiar Vim keybindings in emacs, but I actually found it made it more difficult to dive into emacs. Evil-mode is actually impressively complete when it comes to imposing vim functionality over top of emacs, but there are still times when you needto hit `C-x k` or `M-x something-mode` and the cognitive dissonance of switching between them was just overwhelming.

So I'd forego evil-mode and just keep [Emacs Wiki](http://www.emacswiki.org/emacs/) open in your browser for the first few days. It doesn't take that long to dive in head-first.

### Projectile

It ships with Prelude, so not a major headline, but it does help to keep your projects organized and navigate files.

## On Lisp

Since this is really about Clojure development environments, I might as well dive into the inherent Lispiness of emacs. The extension language is a Lisp dialect, and very easy to learn and use. Emacs is so extensible that one of the running jokes is that it's a great operating system in need of a decent text editor. I'll get to that later.

### cider-mode

Interacting with Clojure is amazing with [cider](https://github.com/clojure-emacs/cider). You get an in-editor REPL, inline code evaluation, documentation lookup, a scratch buffer for arbitrary code evaluation, and a dozen other features. LightTable is nice with its InstaRepl but emacs/cider is the real deal. You cannot wish for a better Clojure dev environment... and the community agrees:

<blockquote class="twitter-tweet" lang="en"><p>It&#39;s great to see that <a href="https://twitter.com/hashtag/CIDER?src=hash">#CIDER</a> is still the most popular <a href="https://twitter.com/hashtag/Clojure?src=hash">#Clojure</a> dev environment <a href="https://t.co/inB8bnlyEl">https://t.co/inB8bnlyEl</a> Guess I should release 0.8 soon! :)</p>&mdash; Bozhidar Batsov (@bbatsov) <a href="https://twitter.com/bbatsov/status/525408420489613313">October 23, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

`cider-jack-in` connects to a `lein repl :headless` instance, and `cider-mode` gives you inline evaluation in any Clojure file. It's amazing.

### paredit and smartparens

Ever have trouble keeping your parens balanced? You're covered. [paredit](http://www.emacswiki.org/ParEdit) is the classic solution, but a lot of folks are using [smartparens](https://github.com/Fuco1/smartparens) instead... I've been using smartparens in strict mode and it's made me a lot more disciplined about how I place my forms.


## Other Languages

I've been using Emacs for Ruby, Javascript, Haskell, C++, and so on, and it's been great. The only time I launch another app is when I have to deal with Java, because IntelliJ/Android Studio make life so much easier. But most of that is all the ridiculous build ceremony for Java, so that's neither here nor there.

## EmacsOS

That joke about Emacs being an operating system? Not such a joke.

My favorite Twitter client right now is Emacs [twittering-mode](http://www.emacswiki.org/TwitteringMode). There's Gnus for Usenet and Email, and Emacs 24.4 just came out with an improved in-editor web browser called `eww`.

Emacs is a deep, deep rabbit hole. The only way in is head first. But there's so much you can do in here, and it's a staggeringly powerful environment.

Welcome to the dark side. We have macros.

![Dark Side](/images/post-img/vader-choke.jpg)
