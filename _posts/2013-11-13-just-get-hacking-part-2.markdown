---
layout: post
title: "Just Get Hacking (Part 2)"
date: 2013-11-13 00:09
comments: true
categories: [coding, learning, getting started, new hackers]
---

### The Important Stuff

So [last post](/blog/2013/11/12/just-get-hacking/), I pretty much said "just do it," and explained that the companies you _want_ to hire you will care less about your background than your demonstrable coding skills.

In this post, I want to look a little more closely at the skills that matter, and the specific areas that the "best" (IMHO) companies will focus on. I may be biased, but this is the stuff I care about when I'm interviewing developers (beyond basic coding chops), and I think I'm pretty smart.

### Testing, Testing, Testing

So you're writing code that runs, runs correctly, and runs consistently. That's awesome. But when it comes to writing production code for a real company, you need to _know_ it's correct, in advance. Especially with dynamic languages, when there's no compiler to refuse to build faulty code, testing is paramount.

So when you're working on these little personal projects, and throwing them on [Github](https://github.com), do a few things:

<!-- more -->

* Write tests. If you're using Ruby, I recommend [RSpec](http://rspec.info/).
* Use [Travis CI](https://travis-ci.org/). You'll learn about [continuous integration](http://martinfowler.com/articles/continuousIntegration.html), and it's free for open source.
* Use [Code Climate](https://codeclimate.com/). It's like automated code review, and also free.
* Try [Coveralls](https://coveralls.io/). It'll help you make sure you actually are testing everything.

Plus Travis, Code Climate, and Coveralls will give you little badges for your README.md on Github so you can see how your project is doing at any time.

Read up on practices for [Test-Driven Development](http://en.wikipedia.org/wiki/Test-driven_development), because it matters to the people you really want to work for, and as an aspiring software craftsman, it needs to matter to you.

### Collaboration

I mentioned the importance of coding with others last post, but I can't emphasize it enough. Look for opportunities for pair programming, even if it's remote. There are cool apps you can use for that now, like [Koding](https://koding.com/) (and others), but in a pinch there's always [vim](http://www.vim.org/) and [tmux](http://tmux.sourceforge.net/)... which are tools you'll want to know anyhow. 

And which brings me to my next point...

### Unix or GTFO

Yeah, code is more portable than it has ever been. You can develop Ruby or Clojure or Node.js on Linux, Solaris, OS X, Windows, probably even Haiku... but you need to understand your deployment environment, which is going to be some kind of *nix unless you're doing .NET (which you're clearly not, if you came to me for advice).

In addition, the closer your dev environment is to your production environment, the less risk there is of weird heisenbug inconsistencies.

So learn _some_ kind of *nix, whether it's OS X, Linux, or Solaris, or whatever. And dig down; use the command line. Learn your tools, learn the `git` command line, don't just rely on the Github GUI apps etc. Learn `bash` or `zsh`. Learn how a combination of `find`, `grep`, and `xargs` can save your ass. It'll make your life easier as a developer, and it's vital when it comes to...

### DevOps

Long ago, in a galaxy far, far, away, developers simply wrote application code and the systems that hosted and served that code were managed by a cabal of wizened neckbeards of the Sysadmin clan. Now, in our more enlightened (or is it benighted?) age, development and operations have blurred their lines and DevOps was born.

In many cases, this is just an excuse for developers to be burdened with sysadmin duties; sometimes, it's perfectly sensible as many of the best deployment options are SaaS (Something-as-a-Service) thingamabobs. But it's important to get at least the basics.

So when you're looking for someplace to put your pet project web apps, put them on [Heroku](http://heroku.com). It's free for a single web dyno and no workers, and many of the "add-ons" (like Postgres, Redis, ElasticSearch, etc.) that are technologies you might want to play with have free tiers as well.

[Amazon Web Services](http://aws.amazon.com/) is Level 80 territory as far as I'm concerned, but if you get into the DevOps thing, and want to experiment with tools like [Chef](http://www.opscode.com/chef/), they'll also give you some free time with EC2 instances to play around.

### Summary

It all comes down to "Just Get Hacking". But there are some specifics prereqs for modern software engineering, and if you can make yourself pick those up along the way, all the better. Keep it fun, and keep learning. That's what matters most.
