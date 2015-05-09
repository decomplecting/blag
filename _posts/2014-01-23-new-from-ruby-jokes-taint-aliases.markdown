---
layout: post
title: "New from Ruby Jokes: taint_aliases"
date: 2014-01-23 20:08:13 -0500
comments: true
categories: [ruby, ruby-jokes]
---

The [Ruby Jokes](https://github.com/ruby-jokes) team has a new gem for you that was designed, tested, and released in about an hour this afternoon: [taint_aliases](http://ruby-jokes.github.io/taint_aliases). You can get the full details [on GitHub](https://github.com/ruby-jokes/taint_aliases), but I thought a friendly introduction might make for an enlightening blog post.

### Grundle Your Objects

You see, not everyone prefers the word "taint". Some people are very clinical, and say 'perineum'. Others prefer 'grundle' or 'fleshy fun bridge'. We wanted to give you options, so `taint_aliases` makes a variety of synonyms available to you.

{% img center http://i.imgur.com/7r7Ml5q.png The Most Interesting Taint In The World %}
<!--more-->

With `taint_aliases`, you can do things like this:

{% codeblock lang:ruby %}

require 'taint_aliases'

obj = Object.new

obj.grundle

obj.tainted?

=> true

str = "Foo Bar Baz"

str.fleshy_fun_bridge

str.tainted?

=> true

{% endcodeblock %}

Of course, there are other options, but you can find them in the documentation.

### Roadmap

We're currently at version 0.0.3 of [the gem](https://rubygems.org/gems/taint_aliases), but we plan on adding methods like `Object#ungrundle` and `Object#grundled?` before the 1.0 release.

Pull requests are welcome, and... you're welcome.

P.S. Props to [Micah Gates](https://github.com/mgates) for work on the codebase and to [Milt Reder](https://github.com/milt) for the conception of this gem while we were taking a break at work.

### Update

Thanks to a well-timed pull request from [threeifbywhiskey](https://github.com/threeifbywhiskey), the milestone listed above has been met, and I just pushed v1.0.0 of the gem. w00t!
