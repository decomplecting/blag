---
layout: post
title: "The Polyglot's Dilemma"
date: 2014-12-11 20:58:13 -0500
comments: true
categories: [coding, programming languages, software]
---

If it hasn't been clear up to now, I love [Clojure](http://clojure.org). I wish I could write Clojure all day, every day. But Clojure isn't my first language, and possibly not even the language I grok most completely.

I jump between programming languages all the time, and end up having to do the most jumping at work because I probably have at least a passing familiarity with the most languages for anyone on our team. And that's fine.

What I want to ponder on here is the challenges of "speaking" multiple programming languages, learning new ones, and moving between them.

I started programming BASIC when I was about five years old. By the time I hit high school, I was running Linux and writing Perl, C, and Bash scripts (throw some sed and awk in there for good measure, though one wouldn't call them "languages" as such).

Full disclosure: I have written some PHP. But as the illusory Bertolt Brecht in [_Cradle Will Rock_](http://en.wikipedia.org/wiki/Cradle_Will_Rock) tells the playwright Marc Blitzstein, "Capitalism makes prostitutes of us all."

Okay, back to programming...

<!-- more -->

### The Learning Curve

This is probably the biggest factor in bringing developers on to a new language. "I already know Java, it's enterprisey, and it works, why should I change?" or, "I'm a .NET programmer, who needs anything but C#?"

This is at least 40% of what's wrong with programming today.

I'm not a fan of Java, but I've been writing a good deal of Android code in Java for the past month or so. I'll come back to this, but I want to go down some personal prehistory first.

Several years ago now, I got my first position in which I was the lead developer (well, at first _only_ developer) on a critical OLTP system for a university. I inherited a collection of Perl CGI scripts which, while effective, I viewed as a nightmare to maintain. Luckily, the management at that time (it didn't last) took an attitude of "use the tools you need, just make it work."

So I wrote a comprehensive management toolkit in Ruby on Rails, since Ruby was the next language I learned after Perl (production language; I was playing with Scheme and such as well).

It worked like a charm; I wrote a beloved management interface in Ruby, and then a RESTful API for a legacy system, consumers of that API, and then... an Android app.

Oh, Java. I mean, at least my colleague was stuck writing the Obj-C version for iOS, but still... this was my first encounter with Java since Java 1.1 or whatever in 1999. We made it work. But I was intimidated by the process. Should this be public? static? final? Should I have a public constructor?

### Lrn 2 Polyglot

Yesterday I did a video call with a bunch of students and teachers; third grade, fifth grade, and high school classes.

One of the questions they had was "Is programming simple or complicated?"

My answer was that it's simple to write complicated programs, and complicated to write simple programs.

Languages also present their own challenges re simplicity vs. complexity.

Clojure provides an interesting case as it's intention is "Simple Made Easy", as described in this [talk by Rich Hickey](http://www.infoq.com/presentations/Simple-Made-Easy).

But since it's a hosted language, you end up depending on a lot of Java stdlib packages as well as jars from Maven, etc., and if there isn't an existing Clojure wrapper, you need to know (at least) the public API for the lib and how to handle Java interop.

Understanding Java helps.

Okay, so that's a very specific polyglot use case. But there are more reasons to learn all the things.

So, let's examine Ruby. Ruby has deep roots in Perl, but takes its object model from Smalltalk and incorporates functional constructs from Lisp.

So let's say you have an array of integers:

{% codeblock lang:ruby %}
[1, 2, 3, 4, 5]
{% endcodeblock %}

We can deal with this just like a Perl array:

{% codeblock lang:ruby %}
ary = [1,2,3,4,5]
ary.push 6
=> [1, 2, 3, 4, 5, 6]
ary.pop
=> 6
ary
[1, 2, 3, 4, 5]
{% endcodeblock %}

And if you notice, we used message-passing to do that, so we've fulfilled the Smalltalk model already; we don't call a `pop` procedure, we send the object a `pop` message.

As for the functional aspects...

In Ruby, we would say

{% codeblock lang:ruby %}
ary.select(&:odd?)
=> [1, 3, 5]
{% endcodeblock %}

Whereas in a Lisp like Clojure, the equivalent would be:

{% codeblock lang:clojure %}
(filter odd? [1 2 3 4 5])
=> [1 3 5]
{% endcodeblock %}

### Get to the damn point

Okay, that was some fun code examples. Or maybe not.

There's a certain essential need to be polyglot in today's coding milieu. It's not just mobile, where we have to use Java for Android, Objective-C for iOS, and whatever the hell Windows Phone requires (not that anybody has those).

There are plenty of frameworks like [SenchaTouch](http://www.sencha.com/products/touch/), [Steroids](http://www.appgyver.com/steroids), and so on, for building cross-platform mobile apps with HTML5 and JavaScript.

But when you're building n-tier architectures and also building multiple clients, it's necessary to grok the underlying languages for each piece of the system.

Sometimes that's Java, sometimes it's C or C++, sometimes it's C#. Maybe it's Ada or Forth or Smalltalk or Scheme.

Knowing all the things is important. Today I managed to make a Clojure app segfault and being ableto read the log file (JVM SIGSEGV output) was a necessity.

### No, really, get to the point

Paul Graham has an article that (IMHO) you can't call yourself a "real programmer" unless you've read. Actually, there are several, but especially this one: [Beating The Averages](http://www.paulgraham.com/avg.html)

You learn many languages so you can figure out which one is the most powerful, and which one makes you the best and most effective programmer.

As Graham (correctly) suggests, the most powerful option out there is Lisp. And Clojure is the easiest Lisp to get started with (and offers many advantages over Common Lisp or Scheme) at the moment.

But to really understand why Clojure (or Lisp in general) is worthwhile, you need to understand the pain points of C, C++, Obj-C, Java, Python, Ruby, JavaScript, etc.

Not necessarily all of them, but the moment of enlightenment is so much more explicit when you see what you're being freed from.

### So, the polyglot's dilemma?

You can't run Clojure everywhere... yet.

The [clojure-android](http://clojure-android.info/) project is almost there. There are efforts to use ClojureScript to make prtable applications, and there's even an effort out there somewhere to use Clojure to generate code for iOS. But even with these efforts, one needs to understand the underlying runtime, whether that's Java, Obj-C, or JS.

The truly universal developer has to be a polyglot, and choose the correct implementation for the target. For now, that mostly means "native" to the target, e.g. JAva for Android and Obj-C for iOS. On the server side, we have a bit more leeway.

Eventually, I believe we'll be able to Lisp everywhere, anywhere. Until then, we must be polyglots and willing to write the annoying ocde we wish we could avoid.
