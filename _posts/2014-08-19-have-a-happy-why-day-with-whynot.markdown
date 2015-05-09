---
layout: post
title: "Have A Happy #Whyday with whynot"
date: 2014-08-19 21:26:36 -0400
comments: true
categories: [ruby, jokes, gems]
---

It's August 19th, the day we remember why the lucky stiff's poignant departure
from the internet. [ruby-jokes](https://github.com/ruby-jokes) would hate to
part with the [Whyday](http://whyday.org/) tradition of hacking on something just for fun and releasing
it into the wild.

So it's with great ambivalence we announce [whynot](https://github.com/ruby-jokes/whynot),
a gem that does irresponsible things because... why not?

whynot is for when you really just don't care. It started as a single monkey-patch
to `Kernel`, called `maybe`. `maybe` takes a block, and may or may not yield the
result. So for instance:

{% codeblock lang:ruby maybe %}

maybe do |x,y,z|
  x,y,z = 1,2,3
  x + y + z
end

{% endcodeblock %}

About half the time, this will return `6`. The other half, `nil`.

About three minutes after I pushed whynot to Github, [Micah Gates](https://twitter.com/mi_c_ah)
added some kernel methods that allowed for a little more specificity: `mostly`,
which will execute your code about 2/3 of the time, and `occasionally`, which
has about a 1 in 5 chance of actually executing your code.

#### But wait, there's more!

Just in time for the 0.0.4 release this afternoon, I decided sometimes, the truth
doesn't matter. Or, at least, you just don't care. So I added `meh`. Sometimes
true, sometimes false, whatever. When you really don't care, just do this:

{% codeblock lang:ruby %}

meh ? "I guess" : "Nah."

{% endcodeblock %}

I really wanted to create a global value like `true` or `false` that was neither
truthy nor falsey, but I'm not sure whether that's possible, and I have a feeling
it would require some C-extension hackery if it is.

Perhaps for a future release?

As always, pull requests are welcome, and use at your own risk.
