---
title: Lesson 1 Introduction
---
# Lesson 1: Introduction To Haskell

Brought to you by your beloved (ex)-teaching head.

# Table of Content:

* variables
* types
* operations
* functions
* pairs
* lists

Exercises [here](lesson1_practice.html)

# Variables

Remember in python, this is what happens...

```python
x = 3
x = 4
x = "I don't care what you do here."
```

But haskell is pure!!!

### Purity

In haskell, variables are merely 'nicknames' of values. Furthermore, you can't just give the nickname to someone else. In other words, there cannot be any 'side effects' to anything you do.

```haskell
x :: Int
x = 3
x = 4 -- Error! Redefinition
```

In other words, the `=` sign in haskell works like your mathematical definition - once it is defined, you cannot change it.

# Types

In python, we have `int`, `str`, and `char` data types. It is the same in haskell, except that there are more and they appear in different names

### `Int`

The type `Int` is like the python data type `int`, since they both hold integer values. The difference that the python `int` can hold up to some pretty large values, while this is not the case for haskell. In haskell, `Int` only stores machine sized integers. That is, somewhere near $(\pm 2^{63} )$ depending on your machine. To find the exact size, you can do this:

```haskell
biggestInt, smallestInt :: Int
biggestInt  = maxBound
smallestInt = minBound
```

### `Double`

There is nothing to interesting about `Double`. It is just like the python `float`.

```haskell
d1, d2 :: Double
d1 = 3.14159
d2 = 6.02e23 -- yes, you can use scientific notation
```

### `Char`

A `Char` data type holds a unicode character

```haskell
c1, c2 :: Char
c1 = 'x'
c2 = 'Ø' -- Yes, non ascii also!!
```

Note that a `Char` value must be surrounded with a pair of single quotes.

### `Bool`

A `Bool` data type holds a boolean value(True or False)

```haskell
b1, b2 :: Bool
b1 = True
b2 = False -- Just your plain old stuff
```

### `String`

Strings are just list of characters(we will cover lists later)

```haskell
s :: String
s = "Hello, Haskell!"
```

Note that a `String` values must be surrounded by a pair of double quotes.


# Operations

But what can we do on these data types?

### Arithmetics

You can perform your beloved arithmetics with `Int`, `Integer` and `Double`.

```haskell
ex01 = 3 + 2
ex02 = 19 - 27
ex03 = 2.35 * 8.6
ex04 = 8.7 / 3.1
ex05 = mod 19 3
ex06 = 19 `mod` 3
ex07 = 7 ^ 222
ex08 = (-3) * (-7)
```

Notice something in ex06? The function `mod` is called with the backticks. This is what we call the infix notation. In general, `f a b` is equivalent to this expression: <code> a &#96;f&#96; b</code>

### Arithmetics

But what if you tried this?

```haskell
badArith1 = 1 + 0.1
badArith2 = 1 / 1
```

It turns out that both will result in a syntax error. This is because of the fact that the arithmetic operators can only operate on values of the same time, but you are trying to add a `Int` to a `Double`. The second one will also cause an error because you are trying two `/` two `Int`s, while `/` is only defined for `Double`. To perform `Int` division, you can do this: <code>a &#96;div&#96; b</code>.

### Logic

Nothing is ever complete with the good old logical operators. In haskell, you can manipulate boolean values in the following way:

```haskell
ex11 = True && False -- && means 'and'
ex12 = not (False || True) -- || means 'or'
```

Note that you do not have to put the backticks around `and` because it is defined to be an infix operator. We will cover more on that later. Of course, you can do other things that gives you a boolean result:

```haskell
ex13 = ('a' == 'a') -- (==) tests for equality
ex14 = (16 /= 3) -- (/=) tests for inequality
ex15 = (5 > 3) && ('p' <= 'q')
ex16 = "Haskell" > "C++"
```

You can also do if statements, though it is not very recommended:

```haskell
ex17 = if "Haskell" > "C++" then "Hooray" else "Nooooo"
-- basically: if <cond> then <expr1> else <expr2>
```

# Functions!!!

Haskell is FUNCTIONal, so function does play a big part in the language.

### A Tiny Peek

Here is a very simple function that computes the factorial of an integer:

```haskell
factorial :: Integer -> Integer
factorial 0 = 1
factorial n = n * factorial (n - 1)
```

This may not make sense to you yet, so let's look at it carefully. The first line says that the function maps an `Integer` to another `Integer`. The second line says if the input is a `0`, the return value if `1`. The last line says for any other integers, the return value is the integer `n` multiplied by the factorial of `n - 1`.

For one thing, that looks like math!!!


### Well, yes, that's true.

Haskell functions are indeed like mathematical functions in the sense that they just map one value to another, and we can define them recursively like what I've done above. Besides specifying different rules for different values, we can also use a `guard`:

```haskell
hailstone :: Integer -> Integer
hailstone n
  | n `mod` 2 == 0  -> n `div` 2
  | otherwise       -> 3 * n + 1
```

This looks like the piecewise function mentioned in the H2 Math tutorial. Remember?

### What's that weird line?

In the previous examples, we always write something like ```function1 :: a -> b``` before the actual definition of the function. This is the `type` of functions, which specify what types it accepts as input, and what type its output is.

### There's more...

What if you want more than one argument to the function? Of course you can pass in a pair, or a triplet, but here is an easier way:

```haskell
sumThree :: Integer -> Integer -> Integer -> Integer
sumThree x y z = x + y + z
```
which basically says the function takes in three `Integer`s and return another one. For now, just remember that the type signature goes like:

```haskell
function1 :: t1 -> t2 -> t3 -> ... -> tn -> tr
```

where $(t_1)$ to $(t_n)$ are types of the inputs, and $(t_r)$ is the type of the output.


# Pairs

a.k.a. ships, or couples

### How they work

We can pair two values up using the pair constructor. It looks something like:

```haskell
p :: (Int, Char)
p = (3, 'x')
```

You know what's better? Its value can be extracted using *pattern matching*:

```haskell
sumPair :: (Int,Int) -> Int
sumPair (x,y) = x + y
```

# Lists

The standard stuff

### Examples

```haskell
nums, range, range2 :: [Integer]
nums   = [1,2,3,19]
range  = [1..100]
range2 = [2,4..100]
```

Haskell (like Python) also has list comprehensions; you can read about them [here](http://learnyouahaskell.com/starting-out)

### Strings

Strings are just lists of characters!!!

```haskell
-- hello1 and hello2 are exactly the same.

hello1 :: [Char]
hello1 = ['h', 'e', 'l', 'l', 'o']

hello2 :: String
hello2 = "hello"

helloSame = hello1 == hello2 -- True
```

### Constructing Lists

The simplest list is the empty list:

```haskell
emptyList = []
```

Other lists are built up from the empty list using the `cons` operator, `(:)`. Cons takes an element and a list, and produces a new list with the element prepended to the front.

```haskell
ex18 = 1 : []
ex19 = 3 : (1 : [])
ex20 = 2 : 3 : 4 : []
ex21 = [2,3,4] == 2 : 3 : 4 : []
```


### Functions on Lists

We can apply pattern matching on lists too!

```haskell
-- Compute the length of a list of Integers.
intListLength :: [Integer] -> Integer
intListLength []     = 0
intListLength (x:xs) = 1 + intListLength xs
```

The first part says that the length of an empty list is zero. The second part says that if the input list looks like `(x:xs)`, that is, a first element `x` `cons`ed onto a remaining list `xs`, then the length is one more than the length of `xs`.

# That's it for now

Take your time to absorb :3

Go [here](lesson1_practice.html) for practice!!!
