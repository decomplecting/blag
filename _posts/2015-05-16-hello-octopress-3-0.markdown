---
layout: post
title: "Hello, Octopress 3.0!"
date: 2015-05-16T02:52:43-04:00
categories: blog, coding
---

If you've been here before, my blog probably either looks much cleaner
and less busy, or it looks like git decided to lose all of my layout and
CSS files in some industrial accident. Well, it's no accident, and it's
not (exactly) a redesign.

I was really excited when I the coming of Octopress 3.0 was
[foretold on the Octopress blog][octo30]. New CLI replacing the old
Rake tasks, less obfuscation of the underlying [Jekyll][jekyll] tooling,
and a new gem-based structure for themes, plugins, et cetera. When I saw
[Brandon Mathis' talk at JekyllConf][conftalk], I decided to ready myself
for migration.

This won't be a step-by-step migration guide, but I will go over the
general process that worked (more or less) in my case for migrating to
the new Octopress.

## Out with the new

Starting from scratch with Octopress is dead simple: install the octopress gem,
and then `octopress new my_awesome_blag` and you're ready to go. Like I said,
this isn't a guide, you'll want to [RTFM][rtfm].

The next step (for me) was adding a Gemfile so I could get in on the plugin
goodness, and octopress creates a scaffold for a static Jekyll site _sans_
Gemfile, by default. My Gemfile is pretty simple though; thus far:

{% codeblock lang:ruby Gemfile %}

source 'https://rubygems.org'

gem 'octopress', '~> 3.0.0'


group :jekyll_plugins do
  gem 'octopress-codeblock'
  gem 'octopress-codefence'
  gem 'octopress-image-tag'
  gem 'octopress-quote-tag'
  gem 'octopress-solarized'
  gem 'octopress-social'
  gem 'octopress-linkblog'
  gem 'octopress-filter-tag'
  gem 'octopress-filters'
  gem 'octopress-comment-tag'
  gem 'jekyll-sitemap'
end

{% endcodeblock %}

Pretty much just plugins.

Once I also added them to the `gems` array in my `_config.yml` I was ready
to use them in the blog. Now, how did I know I needed all of those?

## In with the old

Of course, I didn't want to throw away my old blog, I wanted to migrate it.
So for the most part, I just copied the old `blag/source/_posts` folder to
the new `blag/_posts` and my posts were visible to octopress. But of course
I was already using all the old Octopress codeblock, image tag, Disqus, etc.
plugins, I was prepared to have a bad time. Or, at least, go through three
years of blog, post by post. It a lot easier than that, actually. The bulk
of the issues were picked up by running `jekyll serve`, getting an error
message (like 'unknown tag codeblock') and grabbing the right gem to fix it.

That solved most of the problems; codeblocks, blockquotes, and the like were
easy enough to fix. A little fiddling with the templates gave me excerpts on
the index and so on. The default theme isn't perfect, and I kind of miss my
sidebar widgets, but I can live without them. But I was using Disqus for
comments, and the old octopress pull quote plugin, so there was more to do.

## Hand hacking

That subhead is really an exaggeration. Adding the comments back in was as
easy as copying the includes from my old octopress blog, configuring the
appropriate `site.disqus_short_name` and `site.disqus_show_comment_count` vars
in `_config.yml`, and adding the includes to the post template.

The process actually made me really glad I chose to use Disqus for comments;
since I made sure my permalinks were unaltered from my original blog, the
comments were preserved and just popped into place.

Pullquotes were easy as well; I just copied `pullquote.rb` from the old
octopress on Github, popped it in my `_plugins` directory, and Jekyll picked
it right up. If you're using other plugins that haven't made it to the new
octorpess ink gem format, this should work for those as well.

## Moving forward

I'll probably spend a good bit of time tinkering with theming; there's
currently one theme, [genesis][genesis], on the octopress github, but
it's very alpha and not what I was looking for. So hopefully I'll build
something I like, and extract it into a gem if other people seem to like
it too.

Brandon mentioned on Twitter that one big need for 3.0 is documentation.
One of the great things about Octopress in the past was that although it's
a blogging framework for hackers, it was exhaustively documented, making it
really easy to get started. This isn't a migration guide but there needs to be
one. Not sure when I'll have time to help with that, but I probably should.

In the mean time, if you're looking to migrate to Octopress 3.0, I'm happy to
help troubleshoot if I can. Just tweet at me or post in the comments.

[octo30]: http://octopress.org/2015/01/15/octopress-3.0-is-coming/
[jekyll]: http://jekyllrb.com
[conftalk]: https://www.youtube.com/watch?v=KS6e4XxY2H4
[rtfm]: https://github.com/octopress/octopress
[genesis]: https://github.com/octopress/genesis-theme
