---
layout: post
title: A Plethora of Models
subtitle: Now the machine can learn, what should it? And from what data?
date: 2025-10-08
---

This week we read up to frame 17 on page 124 of *The Little Learner*. Despite my laxity with the blog, we have been progressing!

## Recap

At some point in the last few weeks, we put all the pieces together for machine learning via gradient descent. A complete program looks as follows:

```scheme
(with-hypers        ; 1. Choose hyperparameters
    ((revs 1000)    ; 2. Hyperparameter: number of revisions
     (alpha 0.01))  ; 3. Hyperparameter: learning rate
  (gradient-descent ; 4. Learning algorithm: gradient descent
   ((l2-loss line) line-xs line-ys) ; 5. Objective function
   (list 0.0 0.0))) ; 6. Initial guess
```

If you run this code, using the data provided in the book, the output will be:

```scheme
(list 1.0499993623489503 1.8747718457656533e-6) ; 7. Learning!
```

To begin with, let's recap this example. 

### 1. Choose hyperparameters

In machine learning, there is a crucial distinction between "parameters" and "hyperparameters." In a nutshell, "hyperparameters" are supplied by the human programmer, while "parameters" are learned by the program. In `malt`, the MAchine Learning Toolkit included with *The Little Learner*, the `with-hypers` function is provided to help manage the setting of hyperparameters. The function has the following structure:

```scheme
(with-hypers *list-of-hyperparameters* *learning-problem*)
```

In this case, the list of hyperparameters contains two items:

```scheme
((revs 1000) (alpha 0.001))
```

And for the learning problem, we are trying to fit a `line` model to the data in `line-xs` and `line-ys` using gradient descent.

```scheme
(gradient-descent
 ((l2-loss line) line-xs line-ys)
 (list 0.0 0.0))
```

### 2. Hyperparameter: revisions

The first hyperparameter, `revs`, tells the programs how many revisions to perform during training. As we have seen in previous weeks, machine learning proceeds via guesswork. Guess the parameters. Check the guess. Revise the guess. Guess again. Check again. Revise again. And so on. The `revs` hyperparameter tells the program how many times to repeat the cycle.

In this case, `revs` is set to `1000`, so the program will revise the guess $1000$ times before it stops.

In fact this is not the only way to set up a learning problem. In practice, it is also common to set up tolerances for the revisions. For example, there is no point doing all $1000$ revisions if something has gone wrong, and the guess is getting *worse* each time. Likewise, if each guess is only making a tiny improvement on the previous guess, it may be worth stopping the training process early.

But there is a deep reason why it is common to set an arbitrary number of revisions in machine learning. In machine learning, there is often no single correct answer for the problem. There is no single "correct" sentence that ChatGPT should produce in response to your prompt. Instead, there is a wide range of "good enough" answers, and the point is to try and find one of them. If the machine learning is successful, then the program should find a good enough answer in a finite time, and we can just set a certain number of revisions.

In practice, also, training models can be extremely time- and resource-intensive. Large models might require many computers, many hours and many kilojoules to train. The `revs` parameter may therefore be determined by economic or environmental factors, rather than scientific ones.

### Hyperparameter: learning rate

The second hyperparameter, `alpha`, sets the learning rate of the gradient descent algorithm. The learning rate is a tricky concept, which I explained in [a previous post]({% link _posts/2025-07-29-the-uses-of-error.md %}).

The clever idea behind gradient descent is to *learn from error*. But if you try to do this naively, the results will be terrible. The learning rate suppresses the learning process, to ensure the guesses are revised incrementally, and the model doesn't go haywire during training. It should therefore be no surprise `alpha` is a small number, in this case, $0.001$. When you multiply a number by $0.001$, it makes the number $1000 \times$ smaller. In this way, `alpha` ensures that the model improves only a little bit each revision.

### Learning algorithm

Now we move on to the the second part of the expression. We have given the hyperparameters. Now we need to give the learning problem. In `malt`, the first thing you specify is the learning algorthm, in this case, `gradient-descent`. I have already recapped this algorithm, in the discussion of `alpha`. The `gradient-descent` function in `malt` requires two inputs:

```scheme
(gradient-descent *objective-function* *initial-guess*)
```

In this case, the objective function is `((l2-loss line) line-xs line-ys)`, and the initial guess is `(list 0.0 0.0)`.

### Objective function

I explained the objective function [in a previous post]({% link _posts/2025-05-21-how-to-guess.md %}). It is called the objective function because it defines the training objective. In other words, the objective function tells the program what it should try to learn. The objective function itself has three parts:

1. The loss function, in this case `l2-loss`: The program will use this function to test each guess, and measure how inaccurate it is, i.e. to measure the "loss." The `l2-loss` is so called because to calculate it, you square the error, i.e. you raise it to the power of 2.
2. The target function, in this case `line`: This is the template for the model that the function will learn.
3. The training data, in this case `line-xs` and `line-ys`: The program will try to find the right parameters for the target function, so that if you plug a `x`-value into the target function, a quantity close to the corresponding `y`-value will come out.

In this case, the target function is `line`. This is the target function that the authors of *The Little Learner* use for most of the early examples. It is an appropriate target function when you have two variables—a predictor variable (`x`) and an output variable (`y`)—and you think there is a straightforward linear relationship between them. For example, perhaps you predict that the height of a flower (`y`) is determined by how many seconds have elapsed since the seedling burst through the soil (`x`). If you think that flowers grow at a constant rate, then the `line` function would be appropriate.

The `line` function looks like this:

$$
y = wx + b
$$

It has two parameters, `w` and `b`. The aim in machine learning is to find the correct `w` and `b` using the training data. Let's say, for example, you are trying to learn the flower model above. You have some data where lab scientists have measured how tall some flowers are at certain times, and you know when the flowers first appeared as seedlings. Let's say that the seedlings have a minimum height of 1mm when they are first perceived by the human scientist, and they grow roughly at a constant rate of 0.01mm per second. Ideally, if you ran the above code with these data points, the program should learn the following function:

$$
y = 0.01x + 1
$$

In scheme, the output would look like this:

```scheme
(list 0.1 1) ; w, b
```

Using these learned parameters, you could predict how tall a flower would be from the number of seconds that have elapsed. E.g. if the flower is 120 seconds old, you could predict that it will be...

$$
y = 0.01(120) + 1
$$

$$
y = 2.2
$$

millimetres tall. In the machine learning world, such a prediction is called "inference."

Of course, before we do the machine learning, we don't know what the parameters are. In this case, we want the computer to work out what `w` and `b` should be. That leads us to the penultimate part of the example code...

### 6. Initial guess

The initial guess is the starting point for the learning process. In this case, we set `w` to $0$ and `b` to $0$:

```scheme
(list 0.0 0.0)
```

The initial guess is called "little theta" ($\theta$) in *The Little Learner*. The parameters learned by the gradient descent algorithm are called "big theta" ($\THETA$).

When you run the gradient descent algorithm, this initial guess will be improved `revs` times, hopefully producing much better values for `w` and `b`—or for whatever parameters are required by your target function.

### 7. Parameters!

If all goes well, the machine learning program should spit out some new parameters, which can be combined with the target function to start making predictions or inferences. In the [example code](https://github.com/anticodians/little-learner/blob/09370349a8555cacc1304e65e548c4c2dcaa4d9c/5-target-practice.rkt), using the provided `line-xs` and `line-ys`, the learned parameters ($\THETA$) are:

```scheme
(list 1.0499993623489503 1.8747718457656533e-6)
```

If you combine these with the `line` function, you get the following linear equation (rounded to two decimal places):

$$
y = 1.05x + 0.00
$$

Well, if `x` is 72, what would `y` be?

$$
y = 1.05(72) + 0.00

y = 75.6
$$

Or in Scheme, using `malt`:

```scheme
((line 72) ; x = 72
 (list 1.0499993623489503 1.8747718457656533e-6) ; w and b
 )

; 75.59995596389626
```

## A plethora of models

There is an obvious limitation with the example above: the target function. `line` is an extremely simple function. It takes exactly one input, and relates it in a very simple way to the output. It is very easy to think of situations where this target function would be woefully inadequate. Imagine, for example, that you wanted to predict the price of a house. `y` in this case would be an amount in dollars. What `x`-values might you have available? You might know the square footage of the house, the number of rooms, the distance from the CBD, the age of the house, the state of repair, and so on. All of these things might seperately affect the price.

`line` would be hopeless, because you would need a seperate model for each predictor. One `line` the predicts the price based on the number of rooms, another `line` that predicts the price based on the square footage of the house, and so on. Each model would be extremely inaccurate because it only accounts for a single feature of the house. What might work better is a target function like this:

$$
y = w_0 x_0 + w_1 x_1 + w_2 x_2 + ... + w_n x_n + b
$$

In this case, $x_0$ might be the distance from the CBD in kilometres, $x_1$ might be the amount of tree cover in the street, and so on. The model could learn to combine all these factors to predict the overall price, $y$.

In our last session, we saw a target function that could do this, though it was presented differently. The function is called `plane`. It is identical to the function given above, but uses a more compact notation:

$$
y = \begin{Bmatrix} w_0 & w_1 & w_2 & ... & w_n \end{Bmatrix} \dot \begin{Bmatrix} x_0 & x_1 & x_2 & ... & x_n \end{Bmatrix} + b
$$

This is exactly identical to the somewhat simpler notation above. Each of the sets of numbers is a tensor<sub>1</sub>, also known as a vector. This symbol $\dot$ means "dot product." When you take the "dot product" of two vectors, it means that you multiply the corresponding elements (e.g. $w_1 \times x_1$), and then add up all the products. This is of course exactly what we do in the more familiar representation of a linear equation above.

Another example where `line` is an inadequate target function is when the relationship between two variables is non-linear. In visual terms, this means that a graph of the two variables is *curved* rather than *straight*. In this case, the problem is that all the `x` values are raised to the power of $1$. We don't normally write the power when it is a power of $1$, but we can do so to make the point:

$$
y = w_0 x_0^1 + w_1 x_1^1 + w_2 x_2^1 + ... + w_n x_n^1 + b
$$

To allow this line to curve, one or more of these $x$-values can be raised to a power other than $1$, e.g.

$$
y = w_0 x_0^1 + w_1 x_1^2 + w_2 x_2^1 + ... + w_n x_n^k + b
$$

In [the example code](https://github.com/anticodians/little-learner/blob/09370349a8555cacc1304e65e548c4c2dcaa4d9c/5-target-practice.rkt), we looked at the target function `quad`. This is a very simple function, similar to `line`:

$$
y = w_0 x^2 + w_1 x + w_2
$$

Because it contains an $x^2$, it can learn a curved, non-linear relationship between `x` and `y`.

## Target Functions in the Press

In 2017, a new target function was discovered, which triggered the current phase of AI hype: the "transformer," or the T in GPT. We do not have the tools yet to describe the transformer, but we do now know what a target function is, and can appreciate why the discovery of a new target function might be significant. The transformer was initially designed for language modelling: predicting which words should come next based on which have come before. None of target functions we have considered so far, `line`, `quad` and `plane`, are up to this task—though `plane` is getting us closer.

The example of the transformer target function is instructive. It has revolutionised language modelling, allowing engineers to build much more powerful and persuasive models of human speech and writing. It has also revolutionsed image and sound generation. But this algorithm did not arise from linguistic research. It is not based on any insight into the nature of language. It was not chosen because it seems like the ideal target function for capturing how language works. Rather, it was invented primarily to address practical problems with training Large Language Models (LLMs). Basically, when language models get very large, they can become unwieldly. One of the biggest problems is that there can be relationships between words that stretch a very long way through a text, e.g. if the word "Elizabeth" appears at the start of a novel, this increases the chance that the word "Elizabeth" appears at the end of the novel—unless of course the phrase "Elizabeth died" appears halfway through, and so on. In this context, the gradient descent algorithm could grind to a halt, or could be subject to a fiendish issue called "exploding gradients," where the model overcorrects even if you set the learning rate to a very low number. Through some elegant tricks, the transformer model fixed these mathematical issues.

If this is all that the transformer target function did, then how did it enable such progress in LLMs? It did so by speeding up training (through "parrallelisation") and eliminating the pernicious "exploding gradients." These changes allowed LLMs to get much, much larger. Their size increase in three main ways: they could have many many more parameters (billions or trillions of `w`s); they could be trained efficiently on much larger training sets; and they could look at much wider "context windows" (e.g. predicting a word based on the prior million words, instead of the prior 100 or 1000 words). All these changes, in turn, allowed LLMs to produce much more coherent and plausible text.

If we understand the role of the target function, and the criteria by which it is assessed, then we may be in a better position to evaluate claims about progress in AI. Was the discovery of the transformer architecture a "step on the way" to AI? Or was it just an architectural change to some commercial systems that let them run more efficiently...?

## LISP as an expression-language

I love LISP, but are we LISPers wrong to find it elegant? Consider again the key example from the first hundred pages of *The Little Learner*:

```scheme
(with-hypers        ; 1. Choose hyperparameters
    ((revs 1000)    ; 2. Hyperparameter: number of revisions
     (alpha 0.01))  ; 3. Hyperparameter: learning rate
  (gradient-descent ; 4. Learning algorithm: gradient descent
   ((l2-loss line) line-xs line-ys) ; 5. Objective function
   (list 0.0 0.0))) ; 6. Initial guess
```

Wouldn't this be easier in Python? (This code won't work, though it could be made to work)

```python
hyperparameters = {
    "revs": 1000,
    "alpha": 0.01
}

objective_function = make_objective_function(
    target=line,
    loss=l2_loss
    training_x=line_xs,
    training_y=line_ys
)

learned_parameters = gradient_descent(
    objective_function=objective_function,
    hyperparameters=hyperparameters,
    initial_guess=[0.0 0.0]
)
```

The LISP/Scheme/Racket/malt code is extremely concise, and the structure of the code also directly reflects the structure of the program. But is this kind of poetry really the right way to impart knowledge?

It does make me think of some of the great Sanskrit philosophers, such as Nagarjuna and Gangesa, who composed their works in extremely terse couplets (or *shloka*s). The books are almost impossible to read (I've only tried in English translation!), and can only be understood through copious commentary on each highly compressed couplet. One theory is that these poems were used as University curricula. Philosophers would memorise their own poems, or those of their teachers, and recite them to students in class. Each *shloka* would be recited individually, and extensively discussed, as a way to explore the problem. To me, *The Little Learner* hearkens back to this mode of instruction. The code is gnomic and compressed, but it is also fantastically well structured and poetic. The two "voices" in the text discuss the code poetry, and unpack it for the reader. We, the Anticodians, discuss and unpack it further. The only missing piece is the memorisation... and I don't think any of use is up for that!