---
layout: post
title:  "Scala non-sense"
date:   2020-10-05 16:39:24 +0200
categories: scala
---

Here I collect some Scala nonsense. 

# [Case classes][case-classes]

I tried to write:

```
protected case class TransformerContext(symbols: Symbols) { self =>
    val program = inox.Program(s)(symbols)
```

without the `case` but this lead to the following message:

private value ... escapes its defining scope as part of type ...

# [Scala collections][collections]

[An explanation][explanation]

# [Scala online][quick-tests]

# [Scala interpreter][interpreter]

It's benefits are yet unknown to us mortals. 

# Wild traits

Traits are thought as services or as in Java jargon, interfaces, which can be offered to users of a library via "mix-in composition".

## [Self types][self-types]

Using a self type restricts the type of classes in which a trait can be mixed in. 

```
trait A { self: B => ... }
```

## [Self-less trait pattern][selfless]

At some point, the library we build will have many services which will be mixed-in by their users. To avoid code duplication, one can
create convenience traits mixing and perhaps extending the functionality before presented to the end-users. In this process, it is often occur that we get name conflicts, for instance we could get two method with different types which don't overload each other. 

The proposed solution is to mix-in the trait into its companion object and use object import whenever necessary to avoid the clash. 

## [Stackable trait pattern][stackable]

## [Cake pattern][cake]



[self-types]: https://docs.scala-lang.org/tour/self-types.html
[case-classes]: https://docs.scala-lang.org/overviews/scala-book/case-classes.html
[collections]: https://www.scala-lang.org/api/2.12.3/scala/collection/index.html?search=Map
[quick-tests]: https://scastie.scala-lang.org
[explanation]: https://docs.scala-lang.org/overviews/collections-2.13/overview.html
[interpreter]: https://docs.scala-lang.org/overviews/repl/overview.html
[selfless]: https://www.artima.com/scalazine/articles/selfless_trait_pattern.html
[stackable]: https://www.artima.com/scalazine/articles/stackable_trait_pattern.html
[trait]: https://contributors.scala-lang.org/t/using-cake-and-stackable-traits-patterns-together/1560