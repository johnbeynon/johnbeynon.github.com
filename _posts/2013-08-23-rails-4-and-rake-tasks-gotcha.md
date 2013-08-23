---
layout: post
title: "Rails 4 and Rake task gotcha" 
author: John Beynon
tags: Heroku Ruby Rails
---

There's presently a bug in Rails 4.0.0 that can cause you issues deploying your
application to services like Heroku.

In short, a validation such as

```ruby
validates_acceptable_of :terms, allow_nil: false
```

can result in your application becoming undeployable for the first time on
Heroku.

When you do try and deploy it for the first time, gems are bundled etc and then
assets are attempted to be precompiled via a rake task, the problem is that
this fails because Rails isn't doing what it say it's doing in the comment of
production.rb

```ruby
# Eager load code on boot. This eager loads most of Rails and
# your application in memory, allowing both thread web servers
# and those relying on copy on write to perform better.
# Rake tasks automatically ignore this option for performance.
config.eager_load = true
```

At the moment Rails is still loading code so and the particular validation above
requires a database hit to see if the model responds to the virtual attribute -
and being a new application the database doesn't actually exist yet so the
deployment fails.

This has been fixed in [this](https://github.com/rails/rails/pull/11389) pull
request but it's not made it out into general release yet.

A quick fix, if you run into this problem is to not eager load on that initial
deployment, changing it back to true when you've deployed successfully and run
your migrations.


