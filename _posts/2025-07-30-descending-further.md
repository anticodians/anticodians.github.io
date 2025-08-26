---
layout: post
date: 2025-07-30
title: Descending further
subtitle: A name! A name!
---

In this meeting, we reached frame 37 on page 86 of *The Little Learner*.

## Artificial Enlightenment

> This algorithm is known as\
&emsp;*optimization by gradient descent*<sup>&dagger;</sup>\
<sup>&dagger;</sup>Thanks, Augustin-Louis Cauchy (1789-1857)\
\
—*The Little Learner*, p. 86

At the end of our reading last week, we learned the name of the algorithm whose parts have been slowly introduced to us: *optimisation by gradient descent*. The authors of *The Little Learner* attribute this algorithm to a nineteenth-century mathematician, Cauchy.

As I write this, I am on a train without Internet. I can't look up Cauchy and verify his claim to have invented *optimisation by gradient descent*. But the attribution of the algorithm to Cauchy is intriguing. Cauchy, presumably, never studied anything like an Artificial Neural Network (ANN), the kind of model discussed in *The Littler Learner*. Cauchy was not at MIT in the 1960s, when Marvin Minsky and others developed the first ANNs, then called "perceptrons." Cauchy therefore cannot have described how to use gradient descent to set the parameters of an ANN. This work was carried out predominantly by Hinton, Bengio and Lecun, who share a Turing Prize (Hinton also earned a Nobel for this work).

What are the authors of *The Little Learner* trying to tell us, when they attribute this algorithm to Cauchy? This is one of many such attributions in *The Little Learner*, and most of the attributions are to long-dead mathematicians like Cauchy. Presumably *all* the theorems presented in the book were developed by *someone*, but the authors seems to take especial delight in attributing *old* discoveries.

To me, these sardonic references seem to have two implications: machine learning is not new; and it has little to do with technology. Machine learning is a collection of mathematical ideas that have been developed mostly for other reasons over the course of centuries. Implicitly, this history is slow, incremental, and intellectual. Machine learning is not a field of wild Promethean inventions, but a field of patient, humble scholarship. If this is the implication that the authors *The Little Learner* were trying to convey, then they have touched a sympathetic string in the heart of this reader. If not, well, I claim my as a "strong poet" to "misread" their work.[^bloom]

[^bloom]: Thanks, Harold Bloom (I can't look up his dates because, as already mentioned, I'm offline.)

## Revving the Machine

In our session this week, the main content was an implementation of the `revise` function. This function takes three inputs:

1. `f`: the objective function for the model we want to "fit" to the data. As we saw in a previous post, the objective function is a compound of three things: (a) the `x`- and `y`- values of the training data; (b) the loss function that will be used to judge the accuracy of the model when applied to the `x` and `y` values;[^l2_loss] and (c) an empty skeleton of the model, which basically knows how many parameters the model has and how they all fit together.[^line] What `f` is waiting for is the parameters of the model.
2. `revs`: the number of revisions that the `revise` function should attempt. The authors assure us that "a fixed number of `revs` is usually a good approach" with large, complex models such as GPT-4. Basically, with a large model like GPT-4, training is very expensive, and there is not well-defined best answer. So you simply let the training loop run a fixed number of times and hope that the resulting model is good enough.
3. `theta`: the current guess for the parameters of the model.

[^l2_loss]: In our example, the loss function is the "l2 loss," which is based on the squared error.

[^line]: In our example, the skeleton of the model is `line`, which has an extremely simple template: $y = wx + b$. There are always exactly two parameters, `w` and `b` (or $\theta_0$ and $\theta_1$).

In a nutshell, the `revise` function tries to come up with a good set of parameters for the model. First it plugs `theta` into `f` to calculate the loss. Then it uses the loss to improve `theta`, and goes back to the start. It plugs the new `theta` into `f` to calculate the loss. Then it uses the (new) loss to improve the (new) `theta`, and goes back to the start. It once again plugs the new `theta` into `f` to calculate the loss, and continues until it has improved the guess `revs` times. For the first example of the `revise` function, the authors suggest running it for $1000$ `revs`.

## LISP for Learning

In order to show the `revise` function, the authors have to take a detour into the syntax of Scheme/Racket. They introduce the `map` function, which is needed in order to perform the update on all the parameters in `theta`. As is so often the case, this detour is both elegant and counter-intuitive. The authors ask readers to develop their understanding of recursive functions and their understanding of machine learning at the same time.

Moderating the group, I have found this kind of thing frustrating. I want everyone in the group to enjoy themselves, but the book is periodically quite demanding because of the way it interleaves multiple strands of understanding at once. The subtitle of the book is "A straight line into deep learning," but the book is more like a gradient descent down a bumpy, swerving error curve.

Of course, all technical fields are difficult, because they require learners to master new abstractions. Overall, I find that the authors of *The Little Learner* do a good job of ordering and prioritising their material, and the book certainly appeals strongly to my own imagination. But I wonder if it would be worth hopping off the "straight line" of *The Little Learner* for a session or two, so we could explore the deep links between recursive function theory and AI in general. A detour into the delightful writing of Douglas Hofstadter might be on the cards...

## Notes