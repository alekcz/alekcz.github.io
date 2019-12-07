---
layout: post
title:  "Destructuring keys in clojure"
date:   2019-12-05 09:00:00 +0200
categories: blog
tags: [clojure, destructuring, day 5]
group: dev
---

Oh, you think JSON is your ally? I do a lot work with JSON. So much so that my favourite library is a JSON parsing library ([cheshire](https://github.com/dakrone/cheshire)). The most tedious thing about working wiht JSON is pulling keys out of JSON objects over and over again.  

<iframe src="https://giphy.com/embed/I8SQMuIELiw0w" width="300" height="214" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

Associative destructuring is the hero we need but don't deserve. It's syntactic sugar for extracting keys from an object in a way that makes code more readable. More readable code is more maintainable code. It's made my life much easier.

Given the following map, that was created by parsing a JSON object using [cheshire](https://github.com/dakrone/cheshire):
```clojure
(def json-object {:fname "Alexander" :lname "Oloo" :handle "alekcz" :location "ZA"})
```

The standard approach to using data from within the map is as follows:

```clojure
(defn twitter-link [user]
    (str "<a href='https://twitter.com/" (:handle user) "'>" (:fname user)  " (@" (:handle user) ")</a>")))
(println (twitter-link json-object))
; => <a href='https://twitter.com/'>Alexander (@alekcz)</a>
```
But when we use associative destructuring we get:

```clojure
(defn twitter-link [user]
    (let [{:keys [fname handle]} user]
        (str "<a href='https://twitter.com/" handle "'>" fname " (@" handle ")</a>")))
(println (twitter-link json-object))
; => <a href='https://twitter.com/'>Alexander (@alekcz)</a>
```

Isn't that so much nicer? I think it is. It's a pity I didn't see transit until I was already a man. 


_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).
