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

[self-types]: https://docs.scala-lang.org/tour/self-types.html

