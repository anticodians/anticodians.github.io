---
layout: post
title: Now we have this insight
summary: We (almost) complete our introduction to Scheme and recursive functions.
---

This week we read up to frame 53, on page 16 of *The Little Learner*.[^failure]

[^failure]: Due to a cognitive deficiency of the group leader, we did not actually complete Chapter 0, which we would have had ample time to do...

## The aesthetics of recursion

This week the authors treated us to an extremely concise introduction to the theory of recursion. They presented recursion as a strategy of extreme parsimony. Recursion allows us to write "interesting programs" with *no* loops. Recursion allows us to implement integer addition *without using `+`*. One member of the group marvelled at the resulting programs. He found them *elegant*. Did anyone else?

We discussed more largely the value of parsimony in reasoning. One member of the group observed that parsimony—or elegance—is an aesthetic value that transcends disciplinary boundaries. In a recent article for *Critical Inquiry*, Imogen Forbes-Macphail observes that

> Like mathematicians, literary scholars find beauty in the pursuit of their work; in the products of that work (critical arguments or scholarship); and in the objects of that scholarship, literary artifacts themselves. (2025, p. 481)

Forbes-Macphail is not the first to identify a significant aesthetic dimension in scientific thought, though it is interesting to argue that the aesthetics of mathematical and literary inquiry are similar. What does elegance mean in literary criticism? Do literary critics have the same relish for parsimony as LISP hackers like the authors of *The Little Learner*? Is an interpretation of *The Rover* more powerful if it can be made using fewer concepts? The old debate among creative writing instructors, about the merits of 'minimalist' and 'maximalist' style, rears its head again.

This discussion hearkens back to [Knuth's theory of 'psychological correctness']({% post_url 2024-11-6-psychological-correctness %}), which we discussed last year. I also note Douglas Hofstadter and Melanie Mitchell's brilliant argument about the vitality of 'aesthetic perception' in science, in their jointly-authored chapters for [*Fluid Concepts and Creative Analogies*](https://en.wikipedia.org/wiki/Fluid_Concepts_and_Creative_Analogies).

## Now we have this insight

Several times in the exposition, the authors claim that something "gives us an insight," or that we now "have this insight." "Do we?" quipped one member of the group.

The central conceit of the book is that we, the readers, are identical with the voice in the second column. The second voice models our own experience. Of course, this whole literary structure implies that we *are not* the voice in the second column. The book constantly entreats us to compare ourselves to this model student, and respond to the teacherly voice in the first column in our own way. The irony of the form finds its counterpart in the irony of the reader's response.

## Why do we 'invoke'?

The idea of recursion is that a function "invokes itself." We paused for a while on the idea of "invocation." Why is it that we "call" or "invoke" functions? What is the underlying metaphor?

The discussion recalled to me these famous sentences from the beginning of *The Structure and Interpretation of Computer Programs*:

> The evolution of a process is directed by a pattern of rules called a program. People create programs to direct processes. In effect, we conjure the spirits of the computer with our spells. (1996, p. 2)

One member of the group preferred "invoke" to "call," for the very reason that it implies that the "invoker" has command over the function they summon to their bidding. On the final verge of computation, at the very brink of the machine, when symbols have lost their meaning and the stack trace has buried itself in silicon, the programmer may find herself in the position of Byron's Manfred:

> I have no choice; there is no form on earth\
Hideous or beautiful to me. Let him,\
Who is most powerful of ye, take such aspect\
As unto him may seem most fitting.—Come!

"Come, `add1`!" cries the wizard in his misery. "Come, `add1`, and increment my integer!"

## The efficiency of Scheme

One member of the group asked how it is possible to write efficient programs in Scheme, when recursion is required for all looping.

The answer: [tail-call optimisation](https://en.wikipedia.org/wiki/Tail_call). A topic slightly off the main track of our Critical Code Studies group! But a fascinating one regardless... parsimony strikes again.

## References

Forbes-Macphail, Imogen. “The Four-Color Theorem and the Aesthetics of Computational Proof.” *Critical Inquiry* 51, no. 3 (March 2025): 470–91. [doi:10.1086/734121](https://doi.org/10.1086/734121).

Hofstadter, Douglas R., Daniel Defays, David Chalmers, Robert French, Melanie Mitchell, and Gary McGraw. *Fluid Concepts and Creative Analogies: Computer Models of the Fundamental Mechanisms of Thought*. New York: Basic Books, 1995.

Sussman, Gerald J, Julie Sussman, and Harold Abelson. *Structure and Interpretation of Computer Programs*. Second edition. Cambridge: MIT Press, 1996.

## Notes