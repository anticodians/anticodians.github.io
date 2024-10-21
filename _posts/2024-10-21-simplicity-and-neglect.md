---
layout: post
title: Simplicity and Neglect
summary: Bootstrapping as metaphor for the craft of writing.
---

There have been some interruptions to our group—and the blog—but we are back today. We read slowly through sections `H` and `I` of Knuth's "Literate Programming," which contained some suggestive clues to Knuth's aesthetic philosophy.

## Simplicity: for whom?

Simplicity is Knuth's justification for one-parameter macros:

> Again, I did this in the interests of simplicity, because I noticed that most applications of multiple parameters could in fact be reduced to the one-parameter case. (p. 104)

We discussed this argument for some time, because there is a fascinating lacuna in Knuth's argument: simplicity for whom? Knuth could mean, simplicitiy for the implementor of `WEB` (namely, for Donald Ervin Knuth), or he could mean, simplicity for the user of `WEB`. Knuth's example doesn't clarify the situation. He presents this example of a two-parameter macro:

```
mac(#1, #2) == m[#1*r+#2]
```

and shows how it could be rewritten using only one-parameter macros like so:

```
mac_tail(#) == #]
mac(#) == m[#*r+mac_tail
```

At first blush, the rewritten version looks considerably *more* complicated. It takes more lines of code. It reverses the order of the `[]` symbols, requiring the reader to put them back in the correct order by mentally substituting `mac_tail` for `#]`. Most of us in the group recoiled at first from Knuth's example. Why not allow two-parameter macros, and the apparently more elegant initial example?

On close inspection, some points in favour of Knuth's decision emerged. One of the key simplifications of the rewritten version is that the parameters (`#`) no longer need to be numbered. This is presumably much easier for `TANGLE` to handle, and therefore easier for Knuth to implement. It also eliminates certain possible errors, such as inconsistent labelling, or too many parameters being passed to the macro, or too few.

The main criterion of 'simplicity' for Knuth seems to be: paucity of primitive elements and means of combination. The one-parameter macro comprises one macro label (e.g. `mac_tail`) and one parameter (`#`). There is a simple substitution: replace every `#` on the right-hand side with the passed value of `#`. The two-parameter macro introduces an additional primitive element: the number of the parameter (e.g. the `2` in `#2`). It also introduces an additional substitution rule: first match the parameters on the left and right hand sides using their numbers, then proceed with the substitution.

Programmers often want to 'reason' about their programs. This is probably the activity Knuth hopes to support by allowing only macros of one parameter. It is easier for me to see what a macro will do, because it is so constrained in what it *can* do. I can construct a more complex macro by combining several macros together. While this may seem complex at first, the advantage is that each individual piece is extremely simple, and I can understand it perfectly with little effort.

In this way, there is a happy marriage between the impelementor and the user, both of whom benefit from the same kind of simplicity. How often do programmers and computer scientists aim for this kind of happy marriage? Is the user's simplicitiy alway reducible to the implementors?

Of course in Knuth's case, the users and implementors were often the same people. As he explains in section `I`, on "Portability," installing WEB was no easy matter in the 1980s. This importability extended to programs *written* in WEB, such as TeX. In the days when software was distributed as source code, the user often had to modify the code in order to get the software working. Ease of implementation and ease of use are hard to distinguish in such a context.

We spoke for sometime about the culture of programming in the 1980s. All this fuss about macros seems otiose to digital humanists raised on dynamically typed intepreted languages like R, Python and JavaScript. There is simply no need for all this mucking about! There are two tracks through Knuth's arguments that are difficult to disentangle:

1. Knuth's attempt to overcome the particular limitations of PASCAL, which requires the programmer to write their program in a certain order using certain sections.
2. Knuth's attempt to devise a new form of writing, of general application, which will make software more enjoyable to read and write.

In the context of (1), the discussion of macros is necessary. As Knuth himself demonstrates, some programming tasks are basically just torture in PASCAL without WEB's macros. In the context of (2), however, the discussion seems to wander down the garden path. Is this detail necessary for me to understand the acts of WEAVING or TANGLING code?

## Neglect: bootstrapping the authorial persona

> The `WEB` system caters to system-dependent changes in a simple but surprisingly effective way that I neglected to mention when I listed its other features. (p. 106)

The word 'neglected' evoked a range of responses in the group. There is an obvious fictionality to it. Knuth could of course edit his essay, and introduce this feature earlier on. His essay is obvioulsy artful, and to ascribe the ordering of its contents to 'neglect' is misleading—on the literal level.

But of course Knuth and his readers are well aware of the fictionality of essayistic neglect. The word indicates two aspects of Knuth's writing:

1. His cultivation of Socratic humility.
2. His belief in the linearity of text.

Knuth's humility is an expression of mastery. He can afford to 'neglect' a topic, because he knows when is the right time to introduce it. His writing is replete with such self-effacement. It is easy to imagine his smiling presence in the classroom, as he gently introduces students to theorems that he 'neglected' to tell them earlier on. I personally like this authorial persona—as I like its obvious antecedent, the Socrates of Plato's dialogues. But perhaps his ingratiating humility and pedantic specificity are not to all reader's tastes.

Knuth's belief in linearity expresses his deeper ideas about literacy. For Knuth, the model reader is one who reads a text from the start to the end. The whole `WEB` system is designed to make this possible for software generally. And indeed, how nice it would be if all programs did have a single reading path, so that a new programmer could take a guided tour of the software before they start hacking on it. Knuth is essentially a teacher, and he views the writer's task as pedagogical. Take the reader through the content in the order that it makes sense to human cognition. Avoid complexity and digressions. 'Neglect' what is not necessary to explain until the opportune moment to introduce it.

In this way, Knuth's humility and linearity converge in a common ideal. Both his humility and linearity serve to make the text transparent and open. There is nothing hidden from the reader, at least not intentionally.

There may also be a sly, and thoroghly computational, humour behind Knuth's avuncular language. As one member of the group observed, Knuth himself knows that he hasn't really 'neglected' the topic of change files. Of course he had to neglect it! The contents of the essay have to be in *some* order! It's not possible to write the entire essay in the first sentence! This 'neglect' represents the bootstrapping of the authorial persona. The author writes himself into existence. Knuth didn't 'neglect' the topic of change files until he *introduced* the topic of change files on page 106. Like `TANGLE.WEB`, Knuth's authorial persona is [self-hosted](https://en.wikipedia.org/wiki/Bootstrapping_(compilers)).

We resume next time at section `J. Programs as Webs`, where Knuth's implicit poststructuralism becomes explicit.
