---
layout: post
title: "job_interview"
date: 2012-05-09 13:14
comments: true
categories: [ruby, gems, funny]
---

So, I wanted to plug a little project that
[Micah Gates](https://twitter.com/#!/micahjgates) and I hacked together at
[BohConf](http://railsconf.austinonrails.org/bohconf), the awesome un-conference
 and hackfest that runs parallel to [RailsConf](http://railsconf2012.com) each year.

It's called [job_interview](https://github.com/ruby-jokes/job_interview), and
it's a Ruby gem to automate some of the tedium of programmer job interviews.

As an example, let's take
[FizzBuzz](http://www.codinghorror.com/blog/2007/02/why-cant-programmers-program.html),
a typical interview screening question intended to weed out the applicants who
can't write code to save their lives. In Ruby, you might implement FizzBuzz like
 this:

{% codeblock lang:ruby FizzBuzz  %}

def fizz_buzz(max)
  Array.new(max) do |i|
    j = i + 1
    val  = (j % 3 == 0 ? "Fizz" : "") +
    (j % 5 == 0 ? "Buzz" : "")
    val.empty? ?  j.to_s  : val
  end
end

{% endcodeblock %}

But that's just tedious. With job\_interview, it's dead simple:

{% codeblock lang:ruby job_interview FizzBuzz %}

require 'job_interview'
@answer = JobInterview::Answer.new
@answer.fizz_buzz(5)

 => [1, 2, "Fizz", 4, "Buzz"]

{% endcodeblock %}

It also does Fibonacci sequences (recursive, iterative, and matrix strategies), a quine, the first _n_ primes, and, of course, "Hello, World!"

That wasn't enough, though.

It will also answer the bullshit personal questions that everyone lies about anyway!

{% codeblock lang:ruby %}

include JobInterview::Questions

{% endcodeblock %}

Q. Where do you see yourself in 5 years?

{% codeblock lang:ruby %}

in_5_years

 => "I'd like to have made someone else rich with my re-contextualized non-volatile open architecture."

{% endcodeblock %}

Q. Why do you want to work here?

{% codeblock lang:ruby %}

why_here

 => "Your company has revolutionized seamless next generation interface."

{% endcodeblock %}

Q. Does P = NP?

{% codeblock lang:ruby %}

p_equals_np

 => "I doubt it, but it would make life easier for traveling salesmen."

{% endcodeblock %}

...and many more.

We aim for 100% test coverage with RSpec, so we're confident that this is a
robust solution for a range of job interview scenarios.

We did a lightning talk at RailsConf 2012, and you can
[see the slides here](http://ruby-jokes.github.com/job_interview/pres.html).

Next time you face an interview for a programming job, work smarter, not harder.

`gem install job_interview`
