---
layout: post
title:  "5 Tools for Getting Started with Clojure"
date:   2019-12-02 09:00:00 +0200
categories: [blog]
tags: [clojure, tools, advent of parens, day 2]
group: dev
---

Greetings friend. Today we're going to talk Clojure tools. And no, you don't have to use emacs. There are many tools and they're all slightly different. Which tools are the best? Well, you see, like everything else in programming, it depends. It depends on many things. And therein lies the difficulty. Since our aim is to make it easier for people to enter the Clojure community we're going to evaluate our decisions on beginner friendliness. 

A quick disclaimer: if your primary dev environment is Windows you're in for a world of hurt. I'd strongly recommend getting your hands on a distribution of Unix. It'll make it easier to get help online. 

## The 5 tools
To get started with Clojure you need 5 main tools.

1. An internet connection
1. A terminal
3. A Java SDK
4. A build tool
5. An editor

### 1. An internet connection
Let's be honest, without internet there is very little you can do in tech these days. You'll need internet to download libraries required for your project and to get help when you're stuck.

<div class="tenor-gif-embed" data-postid="14270786" data-share-method="host" data-width="50%" data-aspect-ratio="1.4027777777777777"><a href="https://tenor.com/view/thor-ragnarok-get-help-funny-throw-gif-14270786">Thor Ragnarok Get Help GIF</a> from <a href="https://tenor.com/search/thorragnarok-gifs">Thorragnarok GIFs</a></div><script type="text/javascript" async src="https://tenor.com/embed.js"></script>

The most of the time the libraries are small. The JavaSDK will be the primary data hog in the early days. 

If you're internet situation is dodgy, let chat ~tomorrow~ next week about some possible work arounds.

### 2. A terminal
The default one will do just fine. **#winning**

### 3. A Java SDK
Fortunately or unfortunately, depending on your point of view, Clojure requires Java. And yip there is more than one Java out there. From a beginner perspective, it's almost irrelevant which one you pick. 

Going with [AdoptOpenJDK](https://adoptopenjdk.net/) should create the least drama in your life. It's free, open source, and supported by some [big names](https://adoptopenjdk.net/sponsors.html) such AWS, Microsoft, Red Hat, and IBM to name a few. 

You can install AdoptOpenJDK on OSX like so:
``` bash
$ brew cask install adoptopenjdk
```
And on Linux you can find the instructions for your distro [here](https://adoptopenjdk.net/installation.html)

_If for some reason you ever need to pick a JVM, go with HotSpot. I have not idea which is better, but when in doubt and you have 0 expertise the beaten path is the way to go._

### 4. A build tool
It's very possible to spend hours tinker with config and builds. In the beginning it's very much shooting in the dark. 
[Leiningen](https://leiningen.org/) is easy and straightforward. So for now let's go with that. 

> Leiningen is the easiest way to use Clojure. With a focus on project automation and declarative configuration, it gets out of your way and lets you focus on your code.

Here are some others:
- [Boot](https://boot-clj.com/)
- [clj and deps.edn](https://clojure.org/guides/deps_and_cli)

### An editor
For some obscure reason, editors are a particularly charged topic. We're definitely not getting into that here. Today is a day of peace and tranquility. Unfortunatley, even with lens of beginner friendliness the choice of editor does not become easier. 

The most important thing at this point is to pick an editor that feels comfortable. You'll spend a lot of time in it so choose comfort. 

Here are the top 5 most used editors from [The State of Clojure 2019](https://www.surveymonkey.com/results/SM-S9JVNXNQV/). Pick one:
1. Emacs
2. IntelliJ
3. Vim
4. VS Code
5. Atom

These 5 all have some plugins that make the particularly friendly to Clojure developers, but that is a discussion for another day. 

## A final note
All these recommendations are with the lens of beginner friendliness. As you work in Clojure some of these tools may no longer be fit for purpose and your preferences may change. So don't get too attached. There are enough [emacs zealots](https://twitter.com/bbatsov) out there. 


_May your build always pass._

_Alex_


This post is part of the ["Advent of Parens"](/blog/2019/12/01/advent-of-parens.html).