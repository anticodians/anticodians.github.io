---
layout: post
title: What is, was and shall be
summary: The authors introduce us to β-substitution
---

In our session this week, we continued to learn the basics of the Scheme/Racket programming language, working though pages 4-8 of *The Little Learner*.

As so often happens in close reading, our attention was arrested by an apparently innocuous word: "is." The word "is" has a peculiar meaning in the language of the book. The authors frequently write that something "is" or "is the same as" something else. For example, they pose the question

> What is
> 
>```racket
>(area-of-rectangle 3.0)
>```
>?

The answer:

```racket
(λ (height)
  (* 3.0 height))
```

Or again later:

> The expression
> 
> ```racket
> (add3 4)
> ```
> 
> is the same as
> 
> ```racket
> ((λ (x)
>   (+ 3 x))
>  4)
>```

There is a curious inversion to their presentation. First they present a series of these examples, where s-expressions are evaluated, some involving closures, in which a higher-order function returns a new function that 'remembers' some values passed to the higher-order function. Then, they admit that their use of "is" and "is the same as" is not entirely idiomatic:

>This way of remembering arguments passed in for formals of outer functions inside inner functions is known as β-substitution.

In other words, the word "is" actually means "can be transformed into via β-substitution." Two s-expressions "are the same expression" when they can be transformed in this way. But what does this transformation entail? It entails taking the *name* of something, e.g. `add3`, `height`, `area-of-rectangle`, and replacing it with its *value*. Is "is" the right word for this? Is the *name* of a thing "the same as" the *thing*?

This use of "is" conflicted with intuitions we had in the group. It seems paradoxical to say that the name of something "is the same as" the thing itself. Of course, it is reasonable in the context of evaluating Scheme code. Whenever the code is run, it will be evaluated, so there is a sense in which the code simply *is* what it evaluates to. This sense of "is" also makes sense in an intellectual culture dominated by mathematics. In everyday algebra, there is no real distinction between equality and identity.

$$3 + 2$$

really *is*

$$1 + 4$$

Isn't it? They are equal. Who cares how they are written?[^identity] Seeing this "is", of course, can take some work. How many people can really remember why $$a^2$$ really *is* $$b^2 + c^2$$ in a right triangle?

[^identity]: I'm sure there are varieties of algebra where identity matters—but that is way beyond my knowledge!

In everyday life, we are quite happy to "dereference" or "substitute" names for the things themselves. When I ask you to "pass the pepper," I'm quite happy when you hand me the pepper grinder. You ask, "Is this what you wanted?" I reply, "Yes, it *is*!"

But nonetheless there is something alarming in being told that two things "are" one another when you haven't internalised the substitution process that allows you to move between them. And names *do* have a reality of which we are sometimes reminded. If I ask a Canadian to "pass me the pepper," and they give me a capsicum, I may be disappointed.

The whole discussion reminded me of piece by Lewis Carroll, in which a person's name has a name, which itself has a name, which itself has a name, and so on. I was sure that this infinite regress featured in *Gödel, Escher, Bach*, but I have tried and failed to find either the Carroll Story or the Hofstadter variation on it! Is an intimation of a thing the same as the name of a thing? Or is the intimation the thing? Or is the name the intimation? Can a vague recollection be substituted for a textual authority? Or only for a vague apprehension...?

We recommence next week on frame 24, at the top of page 9.