---
layout: post
title:  "Stainless and Inox"
date:   2020-11-10 16:39:24 +0200
categories: links
---

Here are some notes on dealing with some software tools I'm working on. 

# Developing

I described issues building Stainless/Inox [here][build].
[build]: https://github.com/scalameta/metals/issues/2198

I was told of another approach:

1. Check out Inox locally.
2. Make changes and run publishLocal from its sbt project.
3. That produces a new jar locally whose semi-auto-generated name you can see in the sbt output.
4. Substitute that name in stainless's built.sbt and reload the stainless sbt project.

At that point you are using your locally modified version of Inox.

# Version control

[Nightly builds][neutral]

[neutral]: https://en.wikipedia.org/wiki/Neutral_build

# Testing

We use the [sbt testing infrastructure][sbttest] and [scala test][scalatest].

Running it:test runs the so-called integration tests which are configured in build.sbt.

Scenario: To print which tests use the recursion processor.

How to do it: when running the test suite, all files get compiled together.
However, you could pick some function's id and print out fd.getpos.fullString.
That will include the source file path, if known.

[sbttest]: https://www.scala-sbt.org/1.x/docs/Testing.html
[scalatest]: https://www.scalatest.org/user_guide/using_scalatest_with_sbt

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

The Stainless sofware [is documented][stainlessdoc].

[documentation]: https://github.com/epfl-lara/inox/tree/master/src/main/doc
[stainlessdoc]: https://epfl-lara.github.io/stainless/

# Related projects

[Viper][viper]
[viper]: http://viper.ethz.ch/tutorial