---
layout: post
title:  "Fun with Clojure maps"
date:   2019-12-09 07:00:00 +0200
categories: blog
tags: [clojure, maps, day 9]
group: dev
---

There was a time where I was working exclusively in clojure and using SSR for the frontend. It was a peaceful time. But alas peace doesn't last for ever. And then I picked up a new full stack project. A project building a SPA.   

And JSON said to me: _"Peace has cost you your strength. Victory has defeated you"_. 

<iframe src="https://giphy.com/embed/ZwUT5MaDAmMcE" width="300" height="214" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

The hastle of parsing json Node was all too fresh in my memory. Would Clojure be different?

```clojure
(def json { :action "link-profiles", 
            :data { :user "alekcz", 
                    :social { :github "https://github.com/alekcz" 
                              :twitter "https://twitter.com/alekcz"}}})
```

The first time I had to parse a json request I hit a quick google. I was still quite new to Clojure so most problems involved a quick google. And voilà.
![Getting data from within a map"](/images/blog/get.png "Getting data from within a map")

So I tried `get`. And it was ridiculous
```clojure
(get (get (get json :data) :social) :twitter)
```
And when something is unwieldy in Clojure there's probably a more elegant way of doing it. You just need to be willing to look beyond the first google result.  
```clojure
(get-in json [:data :social :twitter])
```
Oh isn't that nice. You gotta love the elegance. To be honest I thought that was as good as it got, until I stumbled across this [gem](https://stackoverflow.com/a/7035984). Turns out you can access data in a map using key like so:
```clojure
(:data json)
; => {:user "alekcz", :social {:github "alekcz", :twitter "alekcz"}}

(:data nil) ; and doing this didn't crash anything.
; nil
```
It was like magic. Immediately it made me think of the [thread-first macro](https://alexanderoloo.com/blog/2019/12/08/clojures-thread-first-macro.html). Maybe? Just maybe we could? Was it too good to be true? Surely not?

```clojure
(-> json :data :social :twitter)
; => "https://twitter.com/alekcz"
```
Sublime. 

<iframe src="https://giphy.com/embed/QRkhoTjSQqfV6" width="300" height="124" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](https://alexanderoloo.com/blog/2019/12/01/advent-of-parens.html).