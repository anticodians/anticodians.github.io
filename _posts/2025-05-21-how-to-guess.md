---
title: How to make a guess
layout: post
summary: We glimpse the outer surface of the algorithm...
---

Today we read up to Chapter 3, Frame 37, on page 67 of *The Little Learner*. You can find the code for the session in the [Github repo](https://github.com/anticodians/little-learner/blob/main/3-slippery-slope.rkt).

## Three steps to learning

So far we have only seen the data structures for deep learning. Today, we started to see how to apply learning algorithms the data.

At a high level, we found that deep learning involves three steps:

1. Guess the function parameters
2. Measure the 'loss'
3. Improve the guess

You keep doing 1., 2. and 3. until finally the 'loss' is nearly $0.0$. At this point, further improvement becomes impossible, and you stop.

## What a guess looks like

The first step is the "guess the function parameters." How do we do this?

For the sake of this chapter, a guess is a list of parameters. Let's say we are trying to fit a straight line to some data. A straight line can be represented by the following function:

$$
f(x) = wx + b
$$

In a machine learning situation, we already know $x$ and $y$ for a large number of entities. What we *don't* know is what $w$ and $b$ should be. So, let's make a guess! We can put $w$ and $b$ together into a list, and call that list $\theta$. In the book, the initial guess was $w = 0.0$ and $b = 0.0$. That results in the following $\theta$:

$$
\theta = (0.0, 0.0)
$$

or, in Scheme/Racket:

```scheme
(define theta (list 0.0 0.0))
```

That's it—a guess is a `list` of numbers. Now the `line` function is very simple. There are only two parameters, $w$ and $b$. A more complex function may have many parameters, and those parameters may have a very complex structure. In the future, `theta` may be a very complex variable—a whole collection of tensors all linked together. But that is, of course, the future.

## How to calculate the loss

So far we have encountered just one "loss function," which allows us to measure how good our latest guess it. The loss function works as follows:

1. Use the current guess for the parameters to produce some predicted `y`-values for the `x`-values in the training set
2. Subtract these predicted `y`-values from the real `y`-values that we already know
3. Square the differences
4. Take the sum of the squares

This is called the "l2 loss". The "2" comes from the fact that we square the errors, which is the same as raising them to the power of 2.

The l2-loss is defined as follows in the text:

```scheme
(define l2-loss
  (lambda (target) ; the function we are trying to 'learn'
    (lambda (xs ys) ; the data: the x-values and y-values we have
      (lambda (theta) ; our current guess for the function parameters
        (let ((pred-ys ((target xs) theta)))
          (sum
           (sqr
            (- ys pred-ys))))))))
```

Since the `target` function and `xs` and `ys` will stay the same throughout the whole training process, we can fix these in place, producing an "objective function." The objective function already knows which function we would like to learn parameters for. It already knows what the `x`-values and `y`-values are in the training data. It is just waiting for some guesses that it can try out. In the session, we tried the following guesses for $\theta$, using `line` as the target function, and some simple points as the `xs` and `ys`:

```scheme
; define objective function
(define objective-function (expectant-function line-xs line-ys))

; try first guess
(objective-function (list 0.0 0.0))
; = 33.21

; try second guess
(objective-function (list 0.0099 0.0))
; = 32.5892403
```

We could keep on trying the algorithm of increasing $\theta_0$ by $0.0099$:

```scheme
(objective-function (list 0.0198 0.0))
; = 31.9743612

(objective-function (list 0.0297 0.0))
; = 31.3653627
```

If you perform this operation 106 times, you get the best possible answer:

```scheme
(objective-function (list (* 106 0.0099) 0.0))
; = 0.13501079999999996
```

If you keep going, the loss starts to go up again. That is, the guesses get *worse*:

```scheme
(objective-function (list (* 107 0.0099) 0.0))
; = 0.13759470000000001
```

As the authors of *The Little Learner* would say, after 107 iterations, we have "overshot" the best possible answer.

## How to improve the guess

Clearly just increasing the $\theta_0$ by $0.0099$ is not a great algorithm for learning the function. It takes many iterations to learn an extremely simple function. Looking at the graph on page 58, the correct function is clearly something very close to $y = (1)x + 0$. Shouldn't this be pretty easy to find? And what if we need to learn $b$ as well as $w$? This algorithm assumes that $b = 0$!

Well, we've not seen a better solution yet, but there are many chapters to go, and many layers left in this onion. Assuredly by the end of all this, we will know the arcana of the field.

## First interlude

Next meeting, we take a break from *The Little Learner* and will look at the [LLM code](https://github.com/rbturnbull/hespi/blob/main/hespi/llm.py) for [HESPI](https://rbturnbull.github.io/hespi/), a fascinating AI-for-GLAM project.