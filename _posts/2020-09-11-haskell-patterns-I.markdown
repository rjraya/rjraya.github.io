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

A lazy cons evaluates only its first argument, while the second argument, the tail, is only evaluated when it is selected.

```
doomedList = [2,3,5,7,undefined]
take 0 xs = []
take n (x:xs) = x : (take (n-1) xs)
main = do print (take 4 doomedList)
```

This feature captures the idea of deferring evaluation in the `proxy pattern`:

> A proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy, extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked. For the client, usage of a proxy object is similar to using the real object, because both implement the same interface. 

Lazy evaluation also allows self-reference. This in turn gives another way of modelling state. Consider the example:

```
randInts' g = (randInt,g) : (randInts' nextGen)
 where (randInt, nextGen) = (generate g)
randInts g = map fst (randInts' g)
main = do
 g <- getStdGen
 print (take 3 (randInts g))
```

If we had not lazy evaluation, then we would have to:

1. Ask for an integer. 
2. Pass a generator. 
3. Receive back integer and new generator. 
4. Start again.

However, above we only have to ask for an integer. This effectively `decouples consumer and producer`. On the other hand, we loose control on when evaluation will happen. This combined with side-effects can lead to problems.

# Monads 

The monad type class can help to `model side effects`: computation that happens to the side of or main computation goal.

```
data Expr = Lit Int | Div Expr Expr

eval :: Expr -> Int
eval (Lit a) = a
eval (Div a b) = eval a `div` eval b

data Try a = Err String | Return a

evalTry :: Expr -> Try Int
evalTry (Lit a) = Return a
evalTry (Div a b) = 
 case (evalTry a) of
  Err e -> Err e
  Return a' -> case (evalTry b) of
   Err e -> Err e
   Return b' -> divTry a' b'

divTry :: Int -> Int -> Try Int
divTry a b = if b == 0
 then Err "Div by Zero"
 else Return (a `div` b)
```

Our code, has to deal with side effects in every step. The monad solution is nicer:

``` 
instance Monad Try where
 return x = Return x
 fail msg = Err msg

 Err e >>= _ = Err e
 Return a >>= f = f a

evalTry' :: Expr -> Try Int
 evalTry' (Lit a) = Return a
 evalTry' (Div a b) = 
  (evalTry' a) >>= \'a ->
   (evalTry' b) >>= \'b ->
    divTry a' b'
```

here we compute a then bind it to 'a, the compute b, bind it to 'b and finally apply the last result. We can even rewrite it using the do notation:

```
do x <- a
   b
= 

a >>= \x -> b

evalTry'' (Lit a) = Return a
evalTry'' (Div a b) = 
 do 
  a' <- (evalTry' a)
  b' <- (evalTry' b)
  divTry a' b'
```
 








 



