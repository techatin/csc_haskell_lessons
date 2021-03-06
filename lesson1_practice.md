---
title: Lesson 1 Exercise
---
# Lesson 1 Exercises: Just Gentle Introductions

This is a shameless rip-off from CIS 192 Spring 13, UPenn. In this exercise, you will write something to validate credit card numbers.

### But how?

All credit card numbers follow some pattern. In particular, if you follow this procedure, you are going to be able to validate a card number:

1. Double every second digit beginning from the right. In other words, double the second last digit, fourth last digit, sixth last digit and so on.

2. Add the digits of the doubled digits and the undoubled ones.

3. The card number is valid if the resultant value is divisible by 10.

The following exercises will guide you through this task. [This](https://gist.github.com/techatin/11709b54d3c786466412852619129f31) is a template to get you started.

### Exercise 1

First, we need to implement a function to convert a number into digits, and another one to return the digits in reverse order. In other words, you have to implement the following functions:

```haskell
toDigits    :: Integer -> [Integer]
toDigitsRev :: Integer -> [Integer]
```

Here's some sample input for your reference:

```haskell
toDigits 1234 == [1, 2, 3, 4]
toDigitsRev 1234 == [4, 3, 2, 1]
toDigits 0 == []
toDigits (-17) == []
```

Hint: you really really only have to create one function. Go search this haskell function called `reverse`!!!

### Exercise 2

Now, we need to double every other digit in the number! We want to double the second last digit, fourth last digit and so on. In other words, implement the following function:

```haskell
doubleEveryOther :: [Integer] -> [Integer]
```

Here's some sample test cases:

```haskell
doubleEveryOther [8, 7, 6, 5] == [16, 7, 12, 5]
doubleEveryOther [1, 2, 3] == [1, 4, 3]
```

Hint: It seems that you can use some pattern matching...

### Exercise 3

Create a function to sum all digits of numbers in a list. In other words, implement the following function:

```haskell
sumDigits :: [Integer] -> Integer
```

Again, here's some sample input for your reference

```haskell
sumDigits [16,7,12,5] == 22 -- 1 + 6 + 7 + 1 + 2 + 5 == 22
```

Hint: Remember `toDigits` from exercise 1? Neither do I.

### Exercise 4

Create a function to validate if an `Integer` is a valid credit card number!!! In short, create this function:

```haskell
validate :: Integer -> Bool
```

Some sample inputs:

```haskell
validate 4012888888881881 = True
validate 4012888888881882 = False
```

Hint: use the previous exercises!!!
