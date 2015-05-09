---
layout: post
title: "Recovering from Clojure/conj"
date: 2014-11-22 20:37:56 -0500
comments: true
categories: [Clojure, Clojure/conj, coding, mindblown]
---

Whew. I just got back from [Clojure/conj](http://clojure-conj.org) and boy, is my brain tired.

I'l be doing a more detailed and code-oriented post with [Milt Reder](https://twitter.com/miltreder) on the [Yet Analytics blog](http://yetanalytics.com/blog) this week, but I need to do a brain dump beofre I brainsplode.

So, getting the fanboy stuff out of the way: I got to shake Rich Hickey's hand and thank him for all the work that went into Clojure and Datomic, i.e., the stuff that made programming fun again for me. So that was fun. This was at the conference party at the [Crime Museum](http://www.crimemuseum.org/), which was a joy and a wonderful place for a party.

But, the actual conj...

<!--more-->

### Brainsplosion: Stage 1

On day one of the conj, I was in awe of the presentations I was seeing. Amazing work in ClojureScript, generative testing, JVM experiments...

I was especially excited to see [Bozhidar Batsov](https://twitter.com/bbatsov) talk about the state of [CIDER](https://github.com/clojure-emacs/cider), since I use it every day in my development cycle with Emacs, and he's also the author of [Prelude](https://github.com/bbatsov/prelude), my baseline Emacs environment. CIDER has come a long way, and it's only getting better. I can't imagine going back to another development environment for Clojure. Although, the talk on [Cursive](https://cursiveclojure.com/) was fascinating, and I'll certainly use it in [IntelliJ](https://www.jetbrains.com/idea/) if I'm writing Java with Clojure wrappers.

Just when I thought I'd had enough: the Rich Hickey keynote, Inside Transducers. This went way deeper than his [Strange Loop talk](https://www.youtube.com/watch?v=6mTbuzafcII).

Rich uses [Aquamacs](http://aquamacs.org/), apparently. Who knew?

Anyhow, I can't go into the meat of transducers here, but I can say they'll mean a massive refactoring of my main codebase, especially when dealing with transformations of data structures from core.async channels. Again, we'll do a more technical post soon. I'm still processing this.

### Brainsplosion: Stage 2

That night there were unsessions, and although there were a number of incredible topics, the one most relevant to our day-to-day (and the one we made it to) was the [Datomic](http://www.datomic.com/) unsession with [Stu Halloway](https://twitter.com/stuarthalloway), one of the architects of Datomic. In less than an hour, the Q&A (only one of the Q's being from me) helped me figure out my deployment strategy for Datomic on multiple peers on AWS behind an ELB instance. I'd been pondering this for months, and it all became clear.

On day 2, we learned some fascinating things about using async channels in ClojureScript, type systems, and Datomic superpowers. I took a break after lunch, and then that night was the party.


### Brainsplosion: Final Meltdown

Today, there were great talks about data pipelines, more generative testing, and then...

I don't even know how to start this.

Let me explain: I came to Clojure with very little Java experience. I learned "enough Java to get by" so I could write simple Android apps. Then I saw this talk by Steve Yegge:

<iframe width="420" height="315" src="//www.youtube.com/embed/tz-Bb-D6teE" frameborder="0" allowfullscreen></iframe>

If you prefer, the [transcript is here](http://steve-yegge.blogspot.com/2008/05/dynamic-languages-strike-back.html).

Did you notice this part?

> So javac, the Java compiler: what does it do? Well, it generates bytecode, does some optimizations presumably, and maybe tells you some errors. And then you ship it off to the JVM. And what happens to that bytecode? First thing that happens is they build a tree out of it, because the bytecode verifier has to go in and make sure you're not doing anything [illegal]. And of course you can't do it from a stream of bytes: it has to build a usable representation. So it effectively rebuilds the source code that you went to all that effort to put into bytecode.

There's way more than that, but that's the first thing that got the JVM raising hairs on the back of my neck.

So anyhow, I've been increasingly interested in JVM internals.

Like how when I first got into Clojure, I learned the main reason it lacked tail call optimization was the JVM's security model.

Yeah. the security model prohibits the reuse of stack frames. I promise, I'll come back to this.


So the closing keynote was by [Brian Goetz](https://twitter.com/briangoetz), Java Language Architect at Oracle. The things I learned about the JVM and where it's going broke my brain more than transducers.

First: we all know (or should know) that Java 8 is getting lambda expressions.

So what happened? Did they add a Function type to the JVM? Nope. Java 8 lambdas are syntactic sugar over interface implementations!

I'm not going to dive into code in this post, as it's my decompression post, but this was one mind-blowing concept.

We also learned that while type erasure in generics isn't going anywhere, we will be able to use generics with primitives. Which is pretty damned cool. So instead of getting the autoboxed `ArrayList<Integer>`, you can get an unboxed `ArrayList<int>`.

I could be wrong, but the move away from autoboxing might allow for more direct access to unboxed primitives from Clojure, which would be a huge win for people who want to, for instance, program OpenGL games in Clojure and need unboxed floats and doubles in order so to do.

But here's the jaw-dropper:

Part of the JVM's security model, ever since the dark days of 1995, has been frame counting. I'm going to get this wrong, so please correct me in the comments. But my understanding is this: If there are 64 frames on the stack, and a new instruction is called, the JVM is going to make sure there are 65 frames on the stack, to prevent frame injection.

This is why we have this `loop` and `recur` bullshit in Clojure. I shouldn't call it bullshit, it's actually an elegant workaround for the limitations of the JVM. But it's still a smelly workaround for the lack of tail call optimization we get in, say, Scheme.

Getting rid of this (in Brian's words, IIRC, **stupid** "security" implementation) means we can drop the prohibition against the reuse of stack frames and actually get tail recursion on the JVM without blowing the stack.

Admittedly, TCO was stated tot be low-priority for the Java language team at Oracle, but if the JVM changes to support it, I don't see why we can't have it in Clojure before Java gets it.

Whew. Brainmelt.

Which also happens to be the least popular sandwich at Denny's.

So there's my immediate Clojure/conj braindump. More will be explicated in posts here and on the Yet blog. But damn was that a good conference.

There were many times I felt like I had to be the stupidest person there.

But most of the people I talked to felt the same, so I guess I'm in good company, and in the right place.
