---
layout: post
title:  "Clojure shootout: keep vs filter"
date:   2019-12-07 09:00:00 +0200
categories: blog
tags: [clojure, filter, keep, day 7]
group: dev
---

_[Oh no, it happened again](https://www.youtube.com/watch?v=_5Zik3jak3A)_    
_it's time to filter or keep_    
_you ponder for hours it's so_  
_you don't know which way to go_  

It doesn't really help that there are two clojure functions that do exactly the same thing. Isn't that PHPs trademark? I've been burned by these twins. One of them is evil. One of them is good. Which is which?

### Keep docs
```clojure 
(keep f) (keep f coll)

"Returns a lazy sequence of the non-nil results of (f item). Note,
this means false return values will be included.  f must be free of
side-effects.  Returns a transducer when no collection is provided."
```

### Filter docs
```clojure 
(filter pred) (filter pred coll)

"Returns a lazy sequence of the items in coll for which
(pred item) returns logical true. pred must be free of side-effects.
Returns a transducer when no collection is provided."
```

From the docs we can see they have the same function signature, they're both lazy, both live in `clojure.core`, they can both produce transducers, and both the applied functions must be free of side effects (yum, clojurey). But if you look a little closer there's a gremlin waiting to hurt you...

Let's try keep the odd numbers less than 10.
```clojure
(keep odd? (range 10))
; => (false true false true false true false true false true)
```

That's not ideal. `keep` told us which numbers to keep but didn't give us the actual numbers. And this is where the gremlin lives. `keep` will return the result of applying to `f` to each element if and only if the result is not `nil`. `f` must then be written specifically to work as such. In others words you can't reuse the transducer you've already written as is. 

```clojure
(keep #(if (odd? %) % false) (range 10))
; => (false 1 false 3 false 5 false 7 false 9)

; keep really needs that nil
(keep #(if (odd? %) % nil) (range 10))
; => (1 3 5 7 9)

; or more concisely (relying on the inner workings of if, eek)
(keep #(if (odd? %) %) (range 10))
; => (1 3 5 7 9)
```

And what does filter do? Exactly what you expect. And that, that is the right thing to do. 

```clojure
(filter odd? (range 10))
; => (1 3 5 7 9) 
; Yay!
```
No matter how whacky you get, it does what you expect. 

```clojure
; you shouldn't do this (not a predicate)
(filter #(if (odd? %) % false) (range 10))
; => (1 3 5 7 9)

; and definitely not this (not a predicate)
(filter #(if (odd? %) % nil) (range 10))
; => (1 3 5 7 9)

; and this is just plain odd (not a predicate)
(filter #(if (odd? %) %) (range 10))
; => (1 3 5 7 9)
```
Filter works even if your predicates are not predicates. Filter has your back either way. And when you're building your confidence in a language, that's important.  


Filter what you don't need. Keeping them is just plain weird. 

<iframe src="https://giphy.com/embed/xUOxeT9vXDpCyNeKsw" width="300" height="300" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).


_* Predicates are functions that given a value return either true or false, based on their internal citeria_