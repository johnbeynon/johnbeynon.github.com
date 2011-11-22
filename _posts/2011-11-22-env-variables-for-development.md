---
layout: post
title: ENV variables for development environment
author: John Beynon
---

Something caught my eye in a recent Heroku newsletter in regards to setting ENV variables in development. The newsletter talks about using [Foreman](https://github.com/ddollar/foreman) for running your application locally which will look for a .env file in the root of your project which should contain key=,value pairs for your variables for development.

Great if you use Foreman, but what about [Pow](http://pow.cx)? Well, no fear - it supports the use of .powrc and .powenv (with .powrc loading first).

In practice it seems like the best solution will be to have a sample_env file under source control for reference and then developers can create either a .env or .powenv file with their own variables off the sample keys - or both (via a symlink from one to the other) which will cover all bases.