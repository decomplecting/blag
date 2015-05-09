---
layout: post
title: "Reify This!"
date: 2014-10-29 01:22:41 -0400
comments: true
categories: [Clojure, coding]
---

On the way home this afternoon I was asked to explain Clojure's `reify` macro, and apparently I did quite well, as an "Aha!" moment resulted. So I shall endeavour to explain `reify` here in the hope that such a moment might be available to others.

Reify derives from the Latin _res,_ or "thing." So `reify` fundamentally means "make a _thing_ out of....

### Protocols and Datatypes

Clojure [protocols](http://grimoire.arrdem.com/1.6.0/clojure.core/defprotocol/) are similar to Java interfaces: They define a set of methods/functions purely by their signatures without providing implementation details. Declaring that a class implements an interface (in Java) or that a record implements a protocol (in Clojure) is a contract that specifies that the given class or record, in order to be valid, will provide concrete implementations of those methods/functions.

But sometimes we don't need a reusable entity with reusable implementations that we can instantiate willy-nilly; sometimes we just need a _thing_ that implements those methods.

In Java, anonymous inner classes can fulfill this purpose. In Clojure, we have `reify.`


### That Nameless Thing

OK, it's not really going to be nameless... let's say we have a putative protocol as follows:

{% codeblock lang:clojure %}
(defprotocol Foo
    (bar [this])
    (baz [this st])
    (quux [this x y]))
{% endcodeblock %}

So if we were creating a new record, we might do:

{% codeblock lang:clojure %}

(defrecord FooRecord
    Foo
    (bar [this] (println this))
    (baz [this st] (str this st))
    (quux [this x y] (str this (* x y))))
{% endcodeblock %}

Which is perfect if we need to repeatedly instantiate a FooRecord that implements the Foo protocol. But sometimes we just need a Foo and be done with it. And so, Clojure gives us `reify`.

<!--more-->

### One-Off Things

Instead of creating a defrecord (I'm going to leave the issue of runtime class generation for another post), we have the option of creating an individual, unique object that implements the desired protocol via `reify`.

Like so:

{% codeblock lang:clojure %}
(def athing
  (reify Foo
    (bar [this] (println this))
    (baz [this st] (str/replace this (re-pattern st)))
    (quux [this x y] (str this (+ x y)))))
{% endcodeblock %}

Now I have `athing` that implements the Foo protocol in a manner appropriate to its context, I don't have to worry about declaring a general case (class, or defrecord), and I can use this object while it's handy and let it get GC'd when I'm done with it.

### Incomplete, and Mostly Wrong

This is a really brief description of the `reify` macro, and more details are available in the [Clojure Grimoire](http://grimoire.arrdem.com/1.6.0/clojure.core/reify/). But it apparently clarified things for one person, so I thought I'd share it here.

But in the words of Steve Jobs...

### And One More Thing...

We've got a Lisp here in Clojure, right? We're doing functional programming, so why all of this larking about with objects?

It's not just Clojure's Java heritage. Forms like `defrecord`, `defprotocol`, and `reify` aren't about Java interop.

Let me take you back in time...

Once upon a time, there was a common Lisp dialect, established by ANSI standard, called Common Lisp.

In the times of mist, the original neckbeards established that this Common Lisp should have an object system, known as [CLOS](http://www.aiai.ed.ac.uk/~jeff/clos-guide.html), or the Common Lisp Object System.

Clojure has an object system as well; some of it seems ties to its underlying Java architecture (at the moment); the emergence of Clojure-CLR and cljs have opened up the possibilities for the object model, maybe?

Not really. OOP models aren't all that creative. Ruby has quite a novel object model but other than that, OOP is pretty boring and let's just forget about that unhappy chapter in our past, shall we?

Let's.
