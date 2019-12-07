---
layout: post
title:  "Clojure Bits: Working with JSON"
date:   2019-09-10 06:00:00 +0200
categories: blog
tags: [clojure]
group: dev
---
Clojure Bits: bite-sized and human friendly bits of Clojure. Today, let’s chat about JSON, the backbone of the internet. I’ve written a ton of web applications in Clojure and so far my favourite library for working with JSON is Cheshire. It’s simple to use and fast. Really fast. Here’s how you can get started with it.

_(This was first published on [medium.com](https://medium.com/@alekcz/clojure-bits-working-with-json-d93660e7b99f))_

## Installation

To install cheshire, add it to you list of dependencies in `project.clj` like so

```clojure
:dependencies [ ...some dependencies...
                [cheshire "5.9.0"] ; installed!
                ...more dependencies...]
```

It’ll download when you use `lein` to run your program or start the REPL .

## Using it

Start by adding cheshire to the current namespace. You can do this in two ways depending on whether you’re working in the REPL or in a file.

```clojure 
In a file =>  (:require [cheshire.core :as json])
In the REPL=> (require '[cheshire.core :as json])
```

## The API

### Clojure map to JSON
```clojure
(json/encode {:message "build passing"})
;; "{\"message\":\"build passing\"}"
```

### JSON to clojure map
```clojure
(json/decode valid-json-object)
;; {message "build passing"}
;; notice the map doesn't have keywords
```

### JSON to clojure map with keywords
```clojure
(json/decode valid-json-object true)
;; {:message "build passing"}
;; Yay, much nicer!
```

Cheshire can do a lot more than this. But this is all you need 99% of the time.

_May your build always pass._

_Alex_

## References
- [https://github.com/dakrone/cheshire](https://github.com/dakrone/cheshire)
- Countless hours of debugging