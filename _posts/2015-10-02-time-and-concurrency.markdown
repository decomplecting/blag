---
layout: post
title: "Time and Concurrency"
date: 2015-10-02T17:18:16-04:00
comments: true
categories: [clojure, programming, talks, datomic]
---

Last Wednesday, I gave a short talk at [Baltimore Innovation Week][biw]
[DevDay][dev], entitled "Time and Concurrency". The slides are hosted
[here][slides], but I'll try embedding them:

<iframe src="http://decomplecting.org/time-and-concurrency" width="800" height="600">
</iframe>

Okay, that seems to work.

I won't recap the entire talk here, as I'm sure I'll be presenting (a revised
version of) it again in the future, but I'll summarize.

### Time

Programmers, especially in the established object-oriented (and imperative)
paradigms, have a problem with time. This isn't a new argument; Rich Hickey
spends most of his talk [Are We There Yet?][awty] problematizing time in
object-oriented programming; even Uncle Bob (Robert C Martin) addresses this in
[Functional Programming; What? Why? When?][fpwww].

I wanted to present the problems with time and concurrency, which are really
problems with state, value, and identity, and how functional programming,
specifically using [Clojure][clj] and [Datomic][dat], allowed us to either
negate or embrace these problems.

Put simply, mutable state is evil. Sometimes a necessary evil, but evil
nonetheless. Even something as simple as assignment:

```ruby
foo = 3
puts foo
=> 3

foo += 1
puts foo
=> 4
```

`foo` is not the foo I started with! We create an identity, `foo`, assign it a
value, and then willy-nilly assign it a new value. Consider:

```clojure
(def foo 3)
(println foo)
=> 3
(println (inc foo))
=> 4
(println foo)
=> 3
```

The function `inc` (increment) doesn't alter `foo`, it simply takes a value, and
returns a new value. This is because `inc` is a **pure** function; it has no
side-effects and cannot alter state.

The problem is that, as Rich Hickey puts it, "object-oriented languages have
no reified notion of time". Objects _change_ over time, but we allow them a
constant identity and have no guarantees (beyond mutexes and locks, which are
the gateway to madness) to ensure that `foo` has the value I expect when I
dereference it.

Pure functions have _no_ concept of time, because having no state, time is
not an issue; they take values and return values, always the same, every time.

### Concurrency

Way back when we only had to consider single-threaded, single-process programs,
time did seem very linear. But in a world of multiple threads in multiple
processes spread across multiple cores, and often multiple machines, running
in parallel, shared mutable state is a huge problem. Pure functions return the
same result, given the same inputs, anywhere they are run, and don't alter
anything. Clojure's emphasis on immutable state, persistent data structures,
and pure functions[^1]. In Clojure, mutable state is [managed][state],
thread-safe, and mutations are always explicit, usually within a transaction.

### Datomic

Datomic takes the ideas of time and immutability and applies them to the
database. Datomic is an EAVT tuple-store, supporting both ACID transactions
and unlimited horizontal read scalability. I highly recommend watching
Rich Hickey's talk [Deconstructing the Database][dtd] for a deep look at
the theory and practice behind Datomic. But in borad strokes, instead of
storing tables of mutable rows and columns (SQL style), or mutable
documents[^2], Datomic stores _facts._ These facts are immutable; if
something changes, a new fact is inserted, or a previous fact is retracted.
That insertion or retraction is stored as a new fact.

This allows Datomic to apply the concept of _time_ to the database; the
previous state of the db as-of any point in time can be queried, and since
the database functionally uses the same persistent data structures as Clojure,
external data can be queried alongside Datomic data as if it were in the
database. This concept of time allows us not only to examine any past state,
but to virtually query the future by adding hypothetical data to our queries.

I won't go into the mechanism of how this all of this is achieved, rather I'll
direct you to the videos on [datomic.com][dat].

### DevDay

DevDay Talks was a really great experience. You can see the full speaker lineup
on the BIW site (linked above). I especially enjoyed [Eric Oestrich][eric]'s
talk on Kubernetes, and Richard McCluskey's dive into DevOps at
[Millenial Media][mm]. So many great talks, and the after party was a lot of
fun too. Thanks to [Baltimore Innovation Week][biw] and
[Technical.ly Baltimore][tb] for throwing such a great event!


[^1]: "Impure" functions, i.e. those having side-effects, are allowed in Clojure (unlike, say, Haskell), but are the exception rather than the rule
[^2]: Like, e.g., MongoDB or CouchDB

[biw]: http://2015.baltimoreinnovationweek.com/
[dev]: http://2015.baltimoreinnovationweek.com/events/dev_day_talks
[slides]: http://decomplecting.org/time-and-concurrency
[awty]: http://www.infoq.com/presentations/Are-We-There-Yet-Rich-Hickey
[fpwww]: https://www.youtube.com/watch?v=7Zlp9rKHGD4
[clj]: http://clojure.org/
[dat]: http://www.datomic.com/
[state]: http://blog.jayfields.com/2011/04/clojure-state-management.html
[dtd]: https://www.youtube.com/watch?v=spMU2tECscM
[eric]: https://twitter.com/ericoestrich
[mm]: http://www.millennialmedia.com/
[tb]: http://technical.ly/baltimore/
