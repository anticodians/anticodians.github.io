---
layout: post
title: The uses of error
subtitle: Our first step to understanding back-propagation
---

It's been a while since we have met, but we have made progress through *The Little Learner* since our detour into [HESPI](https://rbturnbull.github.io/hespi/). We are steadily moving towards the back-propagation algorithm, the fundamental learning algorithm for all artificial neural networks. We will resume our quest next time on page 78.

The back-propagation algorithm was developed by Geoffrey Hinton, Yoshua Bengio and Yann Lecun, who in 2018 jointly received the Turing Award from the Association for Computing Machinery for their discovery. It is called back-propagation because it propagates the loss back through the neural network. What does this mean? I break it down below.

## Why do we need back-propagation?

As is their wont, the authors of *The Little Learner* do not straightforwardly explain why the back-propagation algorithm is necessary. Instead, they try to reveal this necessity gradually, through their Socratic style.

They begin with a *bad* leaning algorithm: simply pick a parameter of the model, adjust it by an arbitrary amount, and then see if the guess improves. If it improves, do the same thing again. If it doesn't improve, stop—you've reached the best answer you can find. (I covered this algorithm in [a previous post]({% post_url 2025-05-21-how-to-guess %}).)

There are two big drawbacks to this algorithm:

1. You can only adjust one parameter at a time. If you are training GPT-4, with hundreds of billions of parameters, this will be an excruciatingly slow process.
2. The improvement is arbitrary. There is no guarantee that you are changing the right parameter the right amount in the right direction (i.e. should that parameter get bigger by addition or smaller by subtraction?)

Backpropagation remarkably solves both these issues. It allows you to adjust *all* the parameters at once, and it allows you to calculate how much you should increase or decrease each parameter to (more or less) ensure that the model actually improves.

So far we are focussing on drawback 2: working out how much to increase or decrease each parameter. It turns out that you can use the loss function to 

## Three pieces

The **loss** is a measurement of how well the network performs. We have already seen that to train a neural network, you need to define an objective function that the system can use to test itself against the training data. In our reading last session, we found out that you can use this loss to help you improve the network's parameters.

To do this, we were told, you should first calculate the loss, and then multiply it by a new number, the *learning rate* or *rate of change*. The learning rate is necessary because the loss can be very large. If you naively subtract the loss from a parameter, then you are likely to overcorrect the model, and make it *worse*. Thus you multiply the loss by a small number, e.g. $0.0099$, and then use this much smaller number to improve the relevant parameter.

When you take the loss, and use it to adjust the parameters of the model, this is called **propagation**. At the moment, we are working with an extremely simple model, with only two parameters in a single layer. Later, when we encounter more complex models that have many layers of parameters, this idea of **propagation** will make more sense. First you adjust the *last* layer, then the *second last* layer, then the *third last* layer, and so on. Because this process begins in the final layer of the network, and moves back towards the first layer, it is called **back**-propagation.

Of course this implies that there is something called "forward-propagation," and indeed there is such a thing. This is when you push data into the model to produce the output. The data begins in the *first* layer, then the output of the first layer is passed to the *second* layer, and so on, until it reaches the *output* layer.

Thus during training, there is a loop of forward- and back-propagation. First a batch of training data is put into the model. It is propagated *forward* to produce the output, which is this evaluated using the objective function to get the loss. During the back-propagation, the loss is multiplied by the learning rate, and then fed back through the network to adjust all the weights. This is repeated over and over until the network reaches a desired state.

## How humans learn

*The Little Learner* is not only a book about how machines learn, but a book about how humans learn. We have discussed the book's dialogic style and use of Scheme/LISP many times in the Anticodians, and it is safe to say that the authors' view of human learning is controversial. The discussion proceeds logically, and the student's ignorance is (for the most part) modelled by the voice in the second column. But the authors' decision to avoid all foreshadowing (or to use the wanky word, *prolepsis*) does sometimes make the presentation a bit confusing. We are always heading in a direction, but they never tell us what that direction is.

Perhaps they could have taken some inspiration from artificial neural networks and the back-propagation algorithm. When a neural network is trained via back-propagation, it is given all the answers in advance, and then is allowed to find a path towards the answers in small incremental steps. *The Little Learner* might be easier for beginners if they too are provided a picture of the answer before commencing their incremental journey towards it!
