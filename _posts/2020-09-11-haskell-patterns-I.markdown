---
layout: post
title:  "Haskell Design Patterns I"
date:   2020-09-11 16:39:24 +0200
categories: isabelle
---

The building blocks of functional patterns.

The tools: functions, types and lazy evaluation. 

# Recursion

Is more fundamental than types or functions. Since both types or functions can be recursive. 
Recursion can be used as a pattern to `avoid mutable state`. Tail recursion saves space and 
expresses an iterative process. It can be encoded using foldl. 

```
foldl _ v [] = v
foldl f v (x:xs) = foldl f (f v x) xs
```

In foldr, recursion is trapped by f:

```
foldr _ v [] = v
foldr f v (x:xs) = f x (foldr f v xs)
```

# Higher-order functions. 

- Functions are first-class citizens. 
- Functions can be composed. 

Should I use:

```
z x = f (g (h x))
z' x = (f . g . h) x
z'' = f . g . h       <- tacit or point-free programming
```

Use tacit programming when ease of reading is not compromised, i.e. it is easy to infer the types.

- Functions can be currified.

Curried functions are `composable` while uncurried functions are not. 
This is stated in the sense that the functors that operate on the types
of curried functions are expressed with fmap. While more complicated types
require the use of more involved machinery. 

```
square x = x^2
map (map square) ([[1],[2,2],[3,3,3]])
------------------------------------------
let map' = uncurry map
map' (map' square) [[1],[2,2],[3,3,3]]
```

Curried functions allow easy `decoupling`. The site of decoupling is the argument list
By instantiating it with different functions, we get completely different functionality in different parts of the code.

# Types

Algebraic types model combinations (x) and alternations of types (+). This gives an `algebra` of types and thus the name. Pattern matching is the inverse operation which allows to deconstruct a particular algebraic datatype instance. 

Recursive types allow to express the `composite` pattern (TODO: EPFL videos on Design Patterns):

> unify a composite structure with individual members of that structure

example:

```
data Tree a = Leaf a | Branch (Tree a) (Tree a)

size :: Tree a -> Int
size (Leaf x) = 1
size (Branch t u) = size t + size u + 1
```

# Polymorphism

## Parametric polymophism (generic types):

In this case, polymorphism handles an infinite family of types.

```
data Maybe' a = Nothing' | Just' a
length' :: [a] -> Int
length' [] = 0
length' (x:xs) = 1 + length xs
``` 

## Ad-hoc polymorphism (overloading)

In this case, polymorphism handles a finite set of types. There is a guide on what subtype of polymorphism to use (see page 11). 

### Alternation-based ad-hoc polymorphism

```
data Shape = Circle Float | Rect Float Float

area :: Shape -> Float
area (Circle r) = pi * r^2
area (Rect length width) = length * width
```

### Class-based ad-hoc polymophism

```
data Circle = Circle Float
data Rect = Rect Float Float

class Shape a where
 area :: a -> Float

instance Shape Circle where
 area (Circle r) = pi * r^2

instance Shape Rect where
 area (Rect length' width') = length' * width'
```

## Remarks

Because of type information, a compiler can decide statically to what function to dispatch the calls. This can be done for several parameters. So, functional programs allow to express in simple terms the visitor pattern:

> Visitor lets you define a new operation without changing the classes of the elements on which it operates. 

Both parametric polymorphism and ad-hoc alternation-based polymorphism are powerful tools for abstraction. On the other hand, ad-hoc class-based polymorphism is a powerful tool for decoupling.

# Lazy evaluation 


 




 



