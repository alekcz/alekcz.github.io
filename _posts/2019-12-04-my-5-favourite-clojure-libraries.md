---
layout: post
title:  "My 5 favourite clojure libraries"
date:   2019-12-04 09:00:00 +0200
categories: blog
tags: [clojure, libraries, day 4]
group: dev
---

In my travels I have collected a set of clojure libraries that I can rely on to help me solve problems effectively. These are my top 5. 

1. [cheshire](https://github.com/dakrone/cheshire) by [@dakrone](https://github.com/dakrone)
2. [http-kit](https://github.com/http-kit/http-kit) by [@shenfeng](https://github.com/shenfeng) and maintained by [@ptaoussanis](https://github.com/ptaoussanis)
3. [nippy](https://github.com/ptaoussanis/nippy) by [@ptaoussanis](https://github.com/ptaoussanis)
4. [at-at](https://github.com/overtone/at-at) by [@samaaron](https://github.com/samaaron), [@rosejn](https://github.com/rosejn), and [@michaelneale](https://github.com/michaelneale)
5. [charmander](https://github.com/alekcz/charmander) by [@alekcz](https://github.com/alekcz)


### 1. cheshire
cheshire is a library for _"JSON and JSON SMILE (binary json format) encoding/decoding"_.  
I'm currently using `[cheshire "5.9.0"]` successfully in production. 
My favourite thing about cheshire is that when parsing JSON it can automatically convert the keys to keywords in Clojure. I must admit I've abuse this feature in places where I probably shouldn't have. Haha.    

### 2. http-kit
http-kit is a _"minimalist, event-driven, high-performance Clojure HTTP server/client library"_.  
I'm currently using `[http-kit "2.4.0-alpha3"]` successfully in production. #cowboy  
My favourite thing about http-kit is that the HTTP client is really straight forward. Checkout the [docs](http://www.http-kit.org/client.html#options), you'll see what I mean. 

### 3. nippy
nippy is a _"high-performance serialization library for Clojure"_.  
I'm currently using `[com.taoensso/nippy "2.14.0"]` successfully in production. 
My favourite thing about nippy (besides it being rediculously fast) is that after processing large datasets I can save the object straight from memory directly to disk. This allows my application to pick up instantaneously from where it left off after a reboot.  

### 4. at-at
at-at is an _"ahead-of-time function scheduler"_.  
I'm currently using `[overtone/at-at "1.2.0"]` successfully in production. 
My favourite [trick](/blog/2019/09/11/overtone-music-to-keep-my-dynos-awake.html) with at-at is to use it to schedule a ping every 5 minutes to keep my dynos awake. Obviously I use http-kit to do the ping. 

### 5. charmander
charmander is a _"set of libraries to make working with firebase easier in clojure"_.  
I'm currently using `[alekcz/charmander "0.6.0"]` successfully in production.   
My favourite thing about charmander is that it has been the project that has taught me the most about clojure. Writing it has been one heck of a journey.   

_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).
