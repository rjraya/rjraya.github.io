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