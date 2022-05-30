Title: SICP section 1.1-1.2
Date: 2022-05-30 11:17
Category: SICP
Tags: 
Slug: 
Authors: Donald
Summary:  

# On SICP sections 1.1-1.2

The first two sections of SICP cover lots of ground. It starts off explaining the basic syntax of scheme and by the end of 1.2 it expects the reader to be able to implement recursion with ease in scheme. 

Due to the pace at which I must go through the book I will only hit the key concepts that I thought were important.

These key concpets being:

1. Substitution model for Procedure Application

2. Linear recursion and Tree recursion

3. Iteration and tail recursion

## Substitution Model for Procedure Application

Basically the substitution model is the how the book explains how scheme interperets compound expressions. 

There are three steps to this process: 

1. Evaluate the Procedure

2. Evaluate the Arguments

3. Apply the procedure to the arugments

**Note:** The book makes it clear that this is not how the interpreter actually works. Instead it is a model that helps us understand how our programs work.

A good example for this process can be found with the procedure `sum-of-squares`

    :::racket
    (define (sum-of-squares x y)  
         (+ (square x) (square y))) ;;Body of procedure
         (define (square x) (* x x))
    ------------------------
    (sum-of-squares 3 4)

This procedure gets evaluated using the stpes explained above.

1. First  we have `formal parameters x and y` ,
   
   which are called by arguments 3 and 4 in the `sum-of-squares` procedure call.

2. Substitute every occurence of x and y with 3 and 4.

3. `(+ (square x) (square y))` /the body of the procedure becomes `(+ (square 3) (square 4))`

4. Thus the expression directly above reduces to`(+ (* 3 3) (* 4 4)).` using the definition of squares.

5. Applying the multiplications gives `(+ 9 16)`

6. Applying addition gives `25`    

### Applicative Order vs Normal Order

> Definition: Applicative Order- Method of evaluation by evaluating the operator, the operands, and then applying the operator.

> Definition: Normal Order: To not evaluate the operand until the value is needed. 

##### Applicative Order Example

Suppose we have the expression `(square (+ 3 2))`

It would evaluate like this under the rule of applicative order:

    (square (+ 3 2))
    (square 5)
    (* 5 5)
    25

You evaluate the parameter x before you go to the body of square. When you evaluate `(+ 3 2)`, you get 5 and this passed into square. This means `x is bound to 5`. 

##### Normal Order Order Example

    (square (+ 3 2))
    (* (+ 3 2) (+ 3 2))
    (* 5 5)
    25

In normal order you avoid evaluating `(+ 3 2)` until you need to. 

In this case x in `(square x)` is bound to `(+ 3 2)`.

Since you don't evaluate the `(+ 3 2)` until it's needed. You end up needing to evalutate it twice.

With applicative order, since the operand x is evaluated before applying the procedure, you only evaluate `(+ 3 2)` once.

## Iteration and Tail Recursion

Useful links: 

- [Textbook - CS 61AS](https://berkeley-cs61as.github.io/textbook.html)

- [Normal, Applicative and Lazy Evaluation - Kevin Sookocheff](https://sookocheff.com/post/fp/evaluating-lambda-expressions/)
