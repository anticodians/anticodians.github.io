---
title: Is a neuron a line?
layout: post
summary: We (almost) complete the first chapter on machine learning itself...
---

Today we read up to frame 29 on page 27 of *The Little Learner*.[^notquiteagain] You can read/run the code from the chapter in [our github repo for this reading](https://github.com/anticodians/little-learner/blob/ea12b8b3c0961237ad70a142379b3dabd75b73ff/1-the-lines-sleep-tonight.rkt).

[^notquiteagain]: Once again, the moderator of the group didn't look ahead, to realise that the chapter ended on the following page... but the discussion that waylaid us was good in any case.

## $y = wx + b$

In this session, we learned how to represent this familiar function in Racket. The form in which we eventually cast the function was at first sight, rather strange:

```racket
(define line
  (lambda (x)
    (lambda (theta)
      (+ (* (zeroth-member theta) x) ; wx
         (first-member theta)))))    ; b
```

There are three main ways that this representation differs from the $y = mx + b$ we all learned at school:

### First difference: $m$ is $w$

The authors don't tell us why they use $w$ for the coefficient of $x$, rather than the more familiar $m$, but it presumably because the parameters which are coefficients are typically called the "weights" of a model. They left $b$ as is, presumably because the non-coefficient parameters of a model are typically called the "biases." Thus $y = wx + b$ can be read as "$y$ equals $x$ times its weight plus the bias."

### Second difference: $w$ and $b$ are stored in a "tensor":

We've not been introduced to "tensors" yet, but they are implicit in the notation used in the chapter (see page xxiii of the book). For now, a "tensor" is just an array of numbers. In the final version of `line`, `w` and `b` are contained in a single value `theta`, which looks like this: `(tensor w b)`. Since `x` needs to be multipled by `w`, we need to get the "zeroth" member of `theta`: `(zeroth-member theta)`. Since `b` needs to be added to this, we need to get the "first" member of `theta`: `(first-member theta)`.

### Third difference: `line` is not *one* function, but *two*!

We normally think of $y = mx + b$ as a single function. We could rewrite it as $f{x} = mx + b$. But there are *two* `lambda` expressions in `line`, meaning there are *two* functions. What is the deal? The first lambda is a "function maker." As its input, it takes some `x`. It then gives us a new function, where `x` is fixed, and `theta` (i.e. `w` and `b`) aren't known yet. If you plug `theta` into this new function, out will pop the answer.

```racket
(
    (line 10.0)      ; new function, where x=10
    (tensor 4.0 2.0) ; now plug in w=4.0, b=2.0
)
;; answer = 42
```
This is called a "parameterized" function, the authors explain. In an "unparameterized" function, `w` and `b` would be *fixed*. But now we allow the function to change according to some parameters that we give it. It could be $y=7x+3$ or $y=22x -9$ or $y=(z+58)x - (31z)$. Because it is a "parameterized" function, we can try out different "parameters," and let the computer choose the right ones.

## (define<br/>&nbsp;&nbsp;&nbsp;&nbsp;machine-learning<br/>&nbsp;&nbsp;&nbsp;&nbsp;(find-the-right-parameters<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the-machine))

The reason for all this is explained in the book. In machine learning, you usually know $x$ and $y$: this is your 'training data'. The problem is to work out what $w$ and $b$ should be. Hence our `line` function is constructed so that it is given `x` to begin with, and only later is supplied with `w` and `b`. In principle, we could try many different values for `w` and `b`, and see which combination of `w` and `b` produces the correct `y` for a given `x`. If the computer tries out the combinations, and chooses the `w` and `b` for us, then this is called "machine learning."

We had a wide ranging discussion about the 'learning' metaphor in this context. Do linear functions provide a good model of learning? Is it possible that humans "learn" by adjusting activations of neurons in the same manner that a machine learning algorithm adjusts the parameters of a large and complex linear function? The discuss was very wide-ranging, my notes are inadequate, and we have only just scratched the outermost surface of this topic into whose deeps we are about to plunge.

Computer programming is a highly metaphorical pursuit, as the wisest heads in the trade are quick to admit. Programmers' source code is a textual model of the world they are trying to enact in their software. Programmers have different conceptualisations of what they are doing, and the code they write reflects the world-picture that tells them how to write it. Well—these are the ambits of our group, in any case, and the aptness of the "learning" metaphor will be a topic of conversation for many meetings to come...