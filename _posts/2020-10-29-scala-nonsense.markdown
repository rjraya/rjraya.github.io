---
layout: post
title:  "Scala non-sense"
date:   2020-10-05 16:39:24 +0200
categories: git
---

Here I collect some Scala nonsense. 

[Self types][self-types]

```
trait A { self: B => 

}
```

forces functionality of A to be only used by elements of type B. 

It declares a relation A uses B. 

[Case classes][case-classes]

I tried to write:

```
protected case class TransformerContext(symbols: Symbols) { self =>
    val program = inox.Program(s)(symbols)
```

without the `case` but this lead to the following message:

private value ... escapes its defining scope as part of type ...

[self-types]: https://docs.scala-lang.org/tour/self-types.html
[case-classes]: https://docs.scala-lang.org/overviews/scala-book/case-classes.html
