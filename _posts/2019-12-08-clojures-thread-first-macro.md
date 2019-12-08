---
layout: post
title:  "Clojure's thread-first macro: ->"
date:   2019-12-08 09:00:00 +0200
categories: blog
tags: [clojure, thread-first, day 8]
group: dev
---

Don't you just hate functions with names that you can't pronounce. I mean how do you pronounce `->` ? On top of that, its name is not consistent across languages so learning it once is not a guarantee that you'll know its name in another programming language.

In Clojure this, `->`, is the thread-first macro. You're welcome.

```clojure 
(-> x & forms)

"Threads the expr through the forms. Inserts x as the
second item in the first form, making a list of it if it is not a
list already. If there are more forms, inserts the first form as the
second item in second form, etc."
```

### A super practical everyday example
To help us illustrate how the thread-first macro works we need a few functions

```clojure
; let's set everything up
(def ws "wheat-seed")
(defn plant [seed field farm] (str seed "->planted"))
(defn harvest [plant farm] (str plant "->harvested"))
(defn grind [grain machine] (str grain "->ground"))
(defn prepare-dough [flour salt sugar olive-oil] (str flour "->prepared-dough"))   
(defn make-base [dough] (str dough "->made-base"))   
(defn add-toppings [base tomato cheese meat] (str base "->added-toppings"))
(defn bake [dough oven] (str dough "->baked"))
(defn enjoy [pizza] (str pizza "->enjoyed-macro-pizza"))
```

Now let's get threading!

```clojure
;Now lets make a macro pizza
(-> ws
    (plant "far-field" "Old McDonald's Farm") 
    (harvest "Old McDonald's Farm") 
    (grind "stone-mill")
    (prepare-dough "sea-salt" "white-sugar" "ev-olive-oil")
    (make-base)
    (add-toppings "rosa-tomatoes" "mozzarella" "ham")
    (bake "stone oven")
    (enjoy))
```
You'll notice that each function in our pizza maker has one less argument than in its function definition. The first argument is handled by thread-first macro. The thread-first macro takes the output of `ws` and makes it the first argument of `plant` and makes the output `plant` the first argumemt of `harvest`. In other words it does this:

```clojure
(harvest (plant ws "far-field" "Old McDonald's Farm") "Old McDonald's Farm") 
```
And hence its name. It threads previous output as the **first** argument of the next function and continues doing so until it's done. 

The true benefit of the thread-first macro is that it can make code easier to read. You can do your future self a huge favour by using the thread-first macro. Using this macro coupled with naming your functions sensibly makes for code that is a pleasure to read and maintain. 

Happy threading!

<iframe src="https://giphy.com/embed/VIEngKb5u48e35Lxp4" width="300" height="168" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).