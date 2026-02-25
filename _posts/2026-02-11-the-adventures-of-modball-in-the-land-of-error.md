---
layout: post
title: The Adventures of Modball in the Land of Error
summary: The metaphor of learning as a moving object becomes more literal.
---

## Welcoming Mass to the Land of Error

We have resumed our reading of *The Little Learner*. We are in the midst of an explanation of ADAM, or "Adaptive Moment Estimation," which is [a technique for speeding up gradient descent](https://en.wikipedia.org/wiki/Stochastic_gradient_descent#History).

This technique extends the central metaphor of deep learning: gradient descent. In this metaphor, the model is a seeker, searching across the "error surface" for the place of lowest altitude. On the error surface, the high points are erroneous. The low points are correct. The error surface is treacherous terrain. It is pitted throughout with "local optima," apparently deep clefts where the model may get stuck, preventing it from searching the true depths of correctness. One of the tricks of gradient descent is to set up the learning phase so that the model is more likely to end up in a profound crevasse of correct behaviour, rather than a shallow depression of meagre accuracy.

![The Adventures of Modball in the Land of Error](public/img/adventures-of-model-ball.svg)

ADAM extends this metaphor by adding the idea of "momentum" into the gradient descent. In the version of gradient descent we have explored so far, the model has position and velocity, but no mass and therefore no momentum. The model's "position" on the error surface is given by its parameters: depending on how its parameters are set, it will perform better or worse on the training data according to the loss function. Depending on its parameters, it will be higher (wronger) or lower (righter) on the error-surface. The model's "velocity" so far has been given by the gradient of the loss function. When the loss is calculated, some fancy calculus is applied to determine how the parameters should be changed to make it a little more accurate next time. Changing the parameters changes its position on the error-surface. Since a change of position is "velocity," the update function effectively sets the "velocity" of the model in this extended metaphor.

Basically, the way that momentum-based optimisations like ADAM work is this: Each time you update the parameters of the model, remember how you updated it. Then next time, when you calculate the velocity again, you can remember how you changed it last time. As the model move about the error-surface, it effectively "remembers" its prior movements in the same way that a freight train "remembers" it is moving forwards. By retaining some of the previous velocity, the model effectively becomes more "massive," will acquire more "momentum," and will move more quickly in the direction it is already moving. Accordingly, like a freight train, it will barrel over humps and obstacles on the error-surface without being jittered about.

The variable that stores this "momementum" is called $\mu$ ("mu") in *The Little Learner*. $\mu$ is basically $m$, which is the first letter of "momentum" (obviously). The way the learning algorithm "remembers" $\mu$ is by averaging the model's previous velocities. Each time a new training step commences, the new velocity is combined with the average of the old velocities using a "decay rate" that determines how much of the old velocity to mix with the new. The higher the decay rate, the less old velocity is remembered, i.e. the less mass and the less momentum the model has. The lower the decay rate, the more old velocity is remembered, i.e. the *more* mass and the *more* momentum the model has.

Simply incorporating $\mu$ doesn't quite extend the metaphor properly. One aspect of the error-surface, shown in the diagram above, is that the gradient gets less and less—that is, the slope gets shallower and shallower—the closer you get to the bottom of the descent. Since we use the gradient—the slope—to determine the velocity of the model's updates, graident descent tends to slow down the closer the model gets to the end of its descent. This is *not* very similar to a massive object with momentum. So to perfect the metaphor, we change the gradient descent algorithm again. Previously, there was a fixed "learning rate", $\alpha$. If the model is a car, then $\alpha$ is the brakes. As the model rolls down the slope, you multiply the slope by a small number, e.g. $0.001$, so that the model doesn't go careering all over the error-surface like a drunk driver. In the new version of gradient descent, you gradually increase the learning rate. As alpha goes up, it is like taking your foot gradually off the brakes. Thus as the slope gets shallower, the model "brakes" less hard, allowing it to still move quickly towards the beautiful deep valley of intelligence to which it hies.

ADAM means "ADAptive Moment estimation"—or, if you like, "ADAptive Momentum". $\mu$ is the "Momentum" part. The gradual increase of the learning rate is the "ADAptive" part.[^i_think]

[^i_think]: I think! It's been a while since I studied this...

## Precedents

The idea of error as a landscape, through which the earnest seeker travels to the find the truth, is a very old idea. It puts me in mind of *The Faery Queene*. [At the beginning of Book I](https://www.gutenberg.org/files/15272/15272-h/15272-h.htm#canto_I), the Redcrosse Knight and Una lose themselves in the forest of Error:

> Led with delight, they thus beguile the way,\
Untill the blustring storme is overblowne;\
When weening to returne, whence they did stray,\
They cannot finde that path, which first was showne,\
But wander too and fro in wayes unknowne,\
Furthest from end then, when they neerest weene,\
That makes them doubt their wits be not their owne:\
So many pathes, so many turnings seene,\
That which of them to take, in diverse doubt they been.

I'm also put in mind of this image, [from a sonnet of Charles Harpur's](https://charles-harpur.org/View/Singleview/?docid=english/harpur/poems/h418&version1=/h418c/layer-final):

> The river that, like a pure mind beguiled,\
Grows purer for its errors

In a forthcoming article for *AI & Society*, I argue that the abstractions of computer programming should be understood as the "virtualisation of metaphor." What I'm getting at is that computer programs make metaphors *real*. Not real in a material sense, but *virtually* real in the way that they shape the behaviour of computers. There is a strain in critical theory that denies any reality to these abstractions (e.g. Galloway, Kittler, Tenen), preferring to see computers materially, as the dance of electrons in silicon. But to me, the metaphorical and virtual dimension is vitally important.

To many people in Silicon Valley today, the "error-surface" is the world, and the Holy Grail of AI lies somewhere deep down, in the farthest and most profound hollow of its mountains and valleys. They take this metaphor extremely seriously, refining and implementing it in the hope of finally creating an AI. But even if it is a fruitful and suggestive metaphor—as Spenser and Harpur prove—it is not the *only* or even necessarily the *best* metaphor. The true path of the quest for intelligence may not lie on the rocky multidimensional landscape of a predefined loss function conditioned on a pre-defined training set!

## Notes
