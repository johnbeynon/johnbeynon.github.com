---
layout: post
title: "Heroku Rails Template" 
author: John Beynon
tags: Heroku Ruby Rails
---

If there's one thing I do a lot of is building Rails applications for deployment
to Heroku. It's also something that my colleagues at [Kyan](http://kyan.com) do.
Keeping up to date with the best practices and Heroku's own recommended best
practices is tough - not to mention configuring your application for a seemless
asset pipeline deploy.

<!--- more --->

So I set about to change that with a Rails template that when applied to a
vanilla Rails application means that given a few edge cases it's almost 100%
guaranteed (I'll give you your money back!) to deploy and run successfully.

My template is both Rails 3 and Rails 4 compatible and determines which version
you have installed when it is invoked by simply doing

```ruby
rails new -m https://github.com/johnbeynon/heroku-rails-template
```

You can see [here](https://github.com/johnbeynon/heroku-rails-template) the full
wdetails of what the template does. Remembering a URL like that isn't particular easy and if it's not easy to
remember you'll forget to use it, so I also whipped up a quick plugin for the
Heroku CLI which you can install via

```
heroku plugins:install https://github.com/johnbeynon/heroku-rails-new.git
```

Once installed you will be able to do:

```
heroku new:rails <appname>
```

and voila, you will have a Rails 3/4 application that's good for deployment to
Heroku.
