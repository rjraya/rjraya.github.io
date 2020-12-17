---
layout: post
title:  "Stainless and Inox"
date:   2020-11-10 16:39:24 +0200
categories: links
---

Here are some notes on dealing with some software tools I'm working on. 

# Developing

I described issues building Stainless/Inox here:
https://github.com/scalameta/metals/issues/2198

I was told of another approach:
Yes, you just check out Inox locally, make changes and then run publishLocal from its sbt project

That'll produce a new jar somewhere locally (whose semi-auto-generated name you can see in the sbt output)

You'll then have to substitute that name somewhere in stainless's built.sbt and reload the stainless sbt project

At that point you'll be using your locally modified version of inox

https://github.com/scalameta/metals/issues/2198

# Version control

Nightly builds: https://en.wikipedia.org/wiki/Neutral_build

# Compilers

What is method `setPos` in:

  abstract class Tree extends utils.Positioned with Serializable {
    def copiedFrom(o: Trees#Tree): this.type = setPos(o)

# Program transformation

There are different flavours including program generation, program analysis and program transformation. Stainless and Inox seem to work on the area of program transformation from which the pervasive program transformers. There are convenient APIs to transform the syntax trees of our programs. 

First, there is a hierarchy of transformers design to capture high-level concepts. Search for transformers in Inox or Stainless. 

Second, there is a convenient API to modify expressions. So this one captures local transformations. 

# Documentation

The Inox API [is documented][documentation]. Do read them on github for quick browsing of markdown. 

[documentation]: https://github.com/epfl-lara/inox/tree/master/src/main/doc