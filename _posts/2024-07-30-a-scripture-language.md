---
layout: post
title: A scripture language
summary: Revelation and authority in computer programming
---

## Cultural literacy

> A moment's thought makes it clear that *ord* changes in a simple way when *j* increases, and that another variable *square* facilitates the updating process. (p. 101)

Literate programming requires literate programmers. Readability is relative. Readers must become literate before they can successfully decode a text, and enter the free world of interpretation.

In this quotation, Knuth once again draws attention to the rationality of his program, its unfolding according to agreed principles of thought. What kind of rationality is this? What principles have been agreed? What does the reader have to know in order to grasp after a "moment's thought" that `j`, `ord` and `square` are related in the way Knuth implies?

Kunth presupposes a certain level of mathematical knowledge in his readers. We discussed the reasonableness of this assumption. Presumably *The Computer Journal* primarily has a readership of academic computer scientists, whose education includes at least one course in number theory. If we presume this audience, then Knuth's gestures of understanding—"A moment's thought makes clear"—are consistent with the literacy of his readers.

Number theory of course remains fundamental to programming in the twenty-first century. The entire edifice of internet communcation rests on encryption algorithms which derive from number theory. Students who undertake degrees in Computer Science surely still acquire this literacy.

But does this assumption square with Knuth's aims? He seems to want literate programs to become part of general literature. He suggests that the program text should make explicit the programmer's thought-process. How much of this thought-process can be left implicit, in a program destined for a general readership?

The audience of programmers is much wider than the audience of computer scientists. In 1984, the concept of "computer literacy" was in the air. Many governments, educational institutions, and visionary programmers believed it was essential for the general public to learn to program. The UK's [Computer Literacy Project](https://clp.bbcrewind.co.uk/) was in full swing. Millions of Britons tuned into televisions programs such as *The Computer Programme* and *Making the Most of the Micro*, which taught viewers how to code in BASIC. More than 150,000 bought *30-Hour BASIC*, a coding course that could be taken independently or via correspondence. Aside from BASIC, other programming languages such as Logo and Smalltalk had been developed for children and hobbyists to use. Number theory, it needn't be stressed, was not a key component of 1980s "computer literacy." It is notable that this notion of "computer literacy" seems not to have informed Knuth's notion of "literate programming."

Modern professional developers, of course, are often data scientists or web developers with little training in mathematics. A front-end developer trying to position a `<div>` correctly is unlikely to know many theorems about the cardinal numbers. Knuth's program arguably makes *incorrect* assumptions about the professionalisation of programmers, even if it makes *correct* assumptions about the literacy of *The Computer Journal*'s readers.

It is probably unfair to criticise this one program of Knuth's. He has selected a particular program which will appeal to a particular readership so he can demonstrate WEB. One could also make a Romantic/modernist argument in favour of Knuth's text: there is a place in literature too for complex texts that address an intellectual few. The world can accomodate *Ulysses* as well as *Treasure Island*. But then, Knuth did seem to set out for the kind of crossover appeal of a Jane Austen...

One member of the group compared Knuth's use of number theory to an eighteenth-century gentleman's use of the Bible. It is simply assumed that the references will make sense. Where does the problem lie... Should we all know number theory? Or should we change religions?

## On complexity

The main aim of sections 11-21 of Knuth's program is to reduce the "time complexity" of the algorithm, as one member of the group noted. The naive algorithm for filtering the primes consumes far more time than is necessary. Knuth steps us through the derivation of Djikstra's prime-number algorithm to explain how it will reduce the complexity of the calculation.

"Complexity" is a word that is used so often in so many different contexts that it is virtually meaningless. Knuth, it must be said, does not actually use the word in this paper.

The naive way to find the primes would result in a more "complex" program, because the program would need to perform more calcuations. But the naive algorithm would result in a much simpler program text: it could be written in fewer lines, and would require much less effot on the part of the reader to understand.

Knuth is a pioneer in the analysis of algorithms, which focusses on the space- and time-complexity of algorithms: that is, how simple they are for the computer to execute. There are other kinds of complexity that computer scientists care about, such as the Solomonoff–Kolmogorov–Chaitin complexity, which is related to how "big" the program is as a set of instructions.

Neither kind of complexity quite explains the readerly experience of programs. The simple-complex distinction is only useful in certain domains. The distinction established by Erich Auerbach between parataxis and hypotaxis as literary styles may be more important. Knuth's text can be hard for a nonspecialist to follow because it is highly hypotactic. Each part of the program radically depends on every other. He uses WEB to manage this hypotaxis, by putting interdependent parts of the program near each other. But if he had found a paratactic style for his program, that required the reader to keep less information in their heads, perhaps our little group of readers may have had an easier time navigating his program text.

We recommence in a fortnight at section 24.