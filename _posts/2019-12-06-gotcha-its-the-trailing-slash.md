---
layout: post
title:  "Gotcha! It's the trailing slash"
date:   2019-12-06 09:00:00 +0200
categories: blog
tags: [clojure, luminus, day 6]
group: dev
---

_You've discovered the [Luminus framework](http://www.luminusweb.net/). You've reached unparalleled levels of productivity. You can build a web app at the drop of a hat. You can't believe no-one told you about this before. You're life is perfect except for one small thing._ 

_Every now and then an existing route returns a 404. It doesn't make sense. The error only occurs some of the time. Should that even be possible? You want to pull you hair out..._

**GOTCHA! It's the trailing slash!**

Luminus relies on the awesome routing library by [reitit](https://github.com/metosin/reitit). And reitit uses exact route matching. So `/apply` and `/apply/` are two different routes. Therefore depending on how your end user enters the url, they may or may not get a 404.

Here's how I fixed it:

```clojure
(mount/defstate app
  ...
      (ring/routes
        (swagger-ui/create-swagger-ui-handler
          {:path   "/swagger-ui"
           :url    "/api/swagger.json"
           :config {:validator-url nil}})
        (ring/create-resource-handler
          {:path "/"})
        (wrap-content-type
          (wrap-webjars (constantly nil)))
        ; Here is it is => 
        (ring/redirect-trailing-slash-handler {:method :strip})
        ;<= and you're good to go
        (ring/create-default-handler
  ...
```

You can learn more about handling the trailing slash [here](https://cljdoc.org/d/metosin/reitit/0.3.10/doc/ring/slash-handler).

_May your build always pass._

_Alex_

This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).

_Today's post is late courtesy of our wonderful electricity provider Eskom. Loadshedding is the best!_