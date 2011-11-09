---
layout: post
title: Increasing Heroku Dynos != More Performance
author: John Beynon
---
Something I keep coming across time and time again is a complete misunderstanding of Heroku Dynos and what increasing the count of them in your application will give you.

Firstly, repeat after me

Increasing Dyno count DOES NOT increase performance

When you give someone a slider the first thing they'll do is put it right to the top as everyone wants everything and then balk at the $828 bill they're going to receive monthly - I've done it and my clients have done it but this is *NOT* increasing performance of your application.

Heroku's definition of a dyno is
A dyno is a single web process running on Heroku. It is capable of serving a single web request (pageview) at a time.

Heroku documents the key concepts of their platform here - but hey, we're developers who don't read no stinking documentation.

In brief, if you have a web page in your application that has a request time of 250ms then a single dyno will be able to process 4 requests a second. If you then increase to 2 dynos you'll be have to process 8 requests a second, 3 dynos - 12 requests a second etc etc. Increasing dyno count increases concurrency NOT performance so it's down to you to get your code as performance as possible, halfing a request time of 250ms to 125ms would double your possible requests per second to 8 so making your code as performant as possible will keep your Heroku bill down since you'll need less dynos.

If your dynos are unable to process the requests then the requests are put into the 'backlog' for later processing as dynos become free. If this backlog becomes too deep and the Heroku platform cannot keep up 'Backlog too deep' messages will be served to your visitors. At this point you have two options, increase your dyno count or make your code more performant.
As Heroku themselves detail - simply adding more dynos to increase concurrency may not be a good thing either if your database cannot keep up with the throughput - this is why when I last spoke with Heroku do not intend to add autoscaling to their platform since if your database is the cause of your backlog then throwing more dynos at your application will only compound the problem. People need to be care of auto scaling options that are coming out whether it be via a gem or a Saas offering.
Mind you, this is all behaviour that your can read about on the Heroku site but I thought I'd add a summary here.

