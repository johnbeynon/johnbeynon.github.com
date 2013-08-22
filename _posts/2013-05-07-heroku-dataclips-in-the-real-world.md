---
layout: post
title: "Heroku Dataclips in the real world" 
author: John Beynon
tags: heroku
---

When Heroku Postgres dataclips first appeared I remembered thinking that they
were pretty cool but was struggling to find a use case for them.

More recently, my opinion has changed to just how awesome they are. Take for
example a recent case where for whatever reason a Heroku worker hadn't been
running for several weeks so the delayed job queue size was quite large.

<!--- more --->

With dataclips this is quite simple to monitor and catch in the future.

1. Define a dataclip which does a count of the delayed_jobs table size

2. Use a service like Pingdom to watch the output of the dataclip and if the
returned content is not a count of 0 then report it. With Pingdom you can set how long a site could be down
so for example setting it to 5 minutes would give the worker plenty of time to
process the queue.

This is only one use of dataclips,  
