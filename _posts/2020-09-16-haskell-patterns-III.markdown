---
layout: post
title:  "Haskell Design Patterns III"
date:   2020-09-16 16:39:24 +0200
categories: haskell
---

Patterns for composition

- Composition features of fundamental type-classes.
- Monad transformers

# Functor

Generalizes function application to work on functorial images of types.

```
class Functor f where
 fmap :: (a -> b) -> f a -> f b
```

fmap obeys these laws:

```
fmap (f . g) == fmap f . fmap g
fmap id == id
```

Example:

```
f ::  Num a => a -> a
f = (^2)

data Maybe' a = Just' a | Nothing'
 deriving (Show)

instance Functor Maybe' where
 fmap _ Nothing' = Nothing'
 fmap f (Just' x) = Just' (f x)

 -- we can do this
 fmap f (Just' 7)
 fmap show (Just' 7)

 -- but not this
 fmap f (Just' "7")
 ```

# Applicative functor

fmap allows only to take one functorial image of type as parameter. Applicative, allows to take several:

```
class (Funtor f) => Applicative f where
 pure :: a -> f a
 (<*>) :: f (a -> b) -> f a -> f b
```
`<*>` obeys a law of composition:

`pure (.) <*> u <*> v <*> w = u <*> (v <*> w)`


Example:

```
import Control.Applicative

data Maybe' a = Just' a | Nothing'
 deriving (Show)

instance Functor Maybe' where
 fmap _ Nothing' = Nothing'
 fmap f (Just' x) = Just' (f x)

instance Applicative Maybe' where
 pure f = Just' f
 Nothing' <*> _ = Nothing'
 _ <*> Nothing' = Nothing'
 (Just' f) <*> (Just' x) = Just' (f x)

pure (,) <*> Just' 2 <*> Just' 3 <-- Just' (2,3)
Just' (.) <*> Just' (+2) <*> Just' (+3) <*> Just' 1 <-- Just' 6
```

Wiki:  an applicative functor is a structure intermediate between functors and monads, in that they allow sequencing of functorial computations (unlike plain functors) but without deciding on which computation to perform on the basis of the result of a previous computation (unlike monads)

# Monad

```
class (Applicative m) => Monad m where
 return :: a -> m a
 (>>=) :: m a -> (a -> m b) -> m b
```

where `>>=` combines a Monad (m a) with a **monadic function** (a -> m b).

Example:

```
import Control.Monad
import Control.Applicative

data Maybe' a = Just' a | Nothing'
 deriving (Show)

...

instance Monad Maybe' where
 return x = Just' x
 Nothing' >>= _ = Nothing'
 (Just' x) >>= f = (f x)
``` 

## Monad as functor and applicative

A monad is more powerful than a functor:

```
liftM :: Monad m => (a -> b) -> m a -> m b
fmap :: Functor m => (a -> b) -> m a -> m b

liftM f m = m >>= return . f

liftM f m = do 
 val <- m
 return (f val)

instance Functor Monad where
 fmap = liftM
```

A monad is more powerful than an applicative:

```
ap mf mx = do 
 f <- mf 
 x <- mx
 return (f x)

instance Applicative Monad where
 pure = return 
 (<*>) = ap
```

the Functor-Applicative-Monad proposal describes a convention on what function to use in each case. 

## Sequencing with Monad and Applicative

Applicative allows sequencing actions that happen in isolation. The only communication allowed is that an action may stop the evaluation of the sequence. 

Monad allows sequences of actions to communicate, i.e. to perform different actions depending on the result of previous actions.

```
action s = do putStrLn s; return s
main = do 
 let actions = map action ["parts", "are", "disconnected"]
 sequence' actions
 return ()

sequence' [] = return []
sequence' (x:xs) = do 
 x' <- x
 xs' <- sequence' xs
 return (x':xs)

sequenceA [] = pure []
sequenceA (x:xs) = (:) <$> x <*> (sequenceA xs)
``` 




