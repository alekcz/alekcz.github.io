---
layout: post
title:  "Overtone: Music to keep my dynos awake"
date:   2019-09-11 21:00:00 +0200
categories: blog
tags: [clojure, overtone]
group: dev
---

In my earlier years, I worked with startups as well as the "idea guys" aka "Code this for me and I'll give you equity in my idea". So I quickly learnt to contain costs for each of the multiple ventures I was involved in. 

I had many misadventures with `nohup`, `upstart`, and `systemctl`. My infrastructure of choice quickly became (and still is) Heroku. No frills. No nonsense. Just `git push`. They have a free plan that could go up to 1000 hours (there are at most 744 hours in a month). All you have to do was verify your account AKA **add your credit card** and you were right as rain. 

![Heroku hobby pricing $0 per month](/images/blog/heroku-dyno-pricing.png "Heroku pricing")

> _"Verified accounts come with a monthly pool of 1000 Free dyno hours; unverified accounts receive 550."_
          
The only slightly annoying thing was that the dyno would sleep after 30 minutes of inactivity. It was more than slightly annoying. Every now and then you'd hit the site or the API and you'd have to cold start the JVM. Not on my watch!

I was pretty new to Clojure at the time and was pretty intimidated by all the complexity of scheduling libraries. So I figured that if I could find a music library (and there must be because Java) surely it would have a metronome or wave generator. And so I found `overtone`: the Open Source toolkit for designing synthesizers and collaborating with music.

After wading through the source code I found the timing part of the library: `overtone.music.time`. My approach was pretty straight forward. I'd run the `interspaced` function and ping the dyno every 5 minutes. 

And so I sang to keep my dynos awake. 

Here's a REPL. 

```clojure
; in your REPL with [overtone "0.10.3"] as a depdency
keepawake.core => (use 'overtone.music.time)
keepawake.core => (defn ping! [] (println "HTTP GET request")) ; this would be the actual get request
keepawake.core => (interspaced 1000 ping!) ; this was originally 300000 milliseconds
```

Eventually, it dawned on me to just use `overtone/at-at` seeing as  `overtone.music.time` was using it anyway.
So these days `at-at` solves all my scheduling needs, while taking me down memory lane to a galaxy far, far away...


_May your build always pass._

_Alex_

## References
- [https://github.com/overtone/overtone](https://github.com/overtone/overtone)
- Reading source code in depth