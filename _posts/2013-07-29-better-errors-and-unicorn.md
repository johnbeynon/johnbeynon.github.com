---
layout: post
title: "Better Errors and Unicorn" 
author: John Beynon
tags: Ruby Rails
---

Nine times out of ten my applications are hosted on Heroku and consequently
following their recommended best practices I use Unicorn webserver for my Rails
applications. 

Ten times out ten I use the [Better Errors](https://github.com/charliesome/better_error) gem to replace the standard Rails
error pages.

<!--- more --->

I'd noticed that on occasions that when I ran into errors during development
that the right panel of Better Errors wasn't populating and I just overlooked it.
It was only when a collegue came to me and said that the error went away when he
switched back to Thin did I start investigating.

Turns out, it's just a case of RTFM - due to the fact that Unicorn has multiple
workers, errors are being handled across different workers and better errors uses
server process memory meaning that the errors aren't available across workers. If
you're using the recommended Heroku unicorn config to control your unicorn
worker count via a environment variable if you set it to 1 for development
then the panel will work again.
