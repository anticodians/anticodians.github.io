---
layout: post
title: The loop is broken
summary: The climax of Knuth's presentation
---

## The inner loop

In this session we concluded the central section of the central section of "Literate Programming". In sections 22-26 of the "woven output," Knuth presents the "inner loop" of his program to print the first 1000 primes. The inner loop checks each candidate number $j$ to see if it is prime. It is the kernel of the program, the part that consumes the most computation time, and which performs the function closest to the program's ultimate goal. And it does it all without performing a single multiplication or division...

We noticed again some common ticks in Knuth's rhetoric. Once again we encounter "the remaining task" (which we had already met in section 11). Once again the program is "quite simple" and "straightforward" (as have been most parts of the program). Knuth's program text unrolls like a function being optimised. It relentlessly converges on its solution, following a chain of logic whose links are joined each to each in an intuitive way. By this point in the program, the whole group were baffled by the mathematics. For this group of humanists, the refrain of *straightforwardness* had become rather humerous.

For my part, I find Knuth's authorial persona amusing, his program elegant, and his presentation of it poetic—to the extent I was able to understand any of them. But others in the group found his authorial persona "judgey," and his presentation of the program intolerably taxing on the powers of memory. What do all these auxiliary variables mean again? What exactly is the structure of that table? How are those different numbers combined? Who exactly was [Eratosthenes](https://en.wikipedia.org/wiki/Eratosthenes), and what does his "sieve" have to do with any of this?

Way back in section 3, Knuth informed us that the program should be "reliable, well motivated, and reasonably fast." We were all amused by the program's final motivation:

> Let's suppose taht division is very slow or nonexistent on our machine. We want to detect nonprime odd numbers, which are odd multiples of the set of primes $\set{p_2, ..., p_{ord}\}$.

We have discussed at many points the *exemplary* nature of the program. Knuth does not intend to provide either a useful program listing (e.g. a prime number solver for use in production), or an exercise in programming style (e.g. an example of structured programming). He intends to provide a well-documented program using WEB, and one gets the impression at many points that the program has been made needlessly complicated simply to justify the need for WEB's features. In this case, the computer's lack of division requires explanation, which requires documentation, which requires—WEB.

## A maze of strands


We took a moment, upon completing the program itself, to reflect on it as a literary work. Most in the group agreed that the WEB program has a remarkably "tangled" structure—to misuse Knuth's own metaphor. You could say that the program is deeply *intratextual*. It constantly refers to itself. No part of the program can very easily be detached, and viewed independently on its own. To understand any part, it is necessary to recall the whole structure of variables and constants that govern its behaviour. The text of the explanation typically refers to code that has not been presented yet. To understand the "motivation" for each programming decision, you need to already understand the program, or at least programs like it. The text is topsy-turvey, round-about, splayed-across and liketty-split. I personally enjoyed the ride, but well-oiled labyrinths are not for everyone!

Upon reading section 27, the index, some of the group were dismayed. (Not really.) If only we had kept the index open the entire time, it might have been possible to keep track of all the quantities and arrays that comprise the program code! But as one member of the group observed, Knuth's preference for mathematical symbolism makes the index unreadable on it's own. What do $c$ and $cc$ mean? You already need an intimate knowledge of the program to understand that they mean "current column" and "columns per page."

Another in the group observed the difficult role that *time* plays in "the plot of the code." The program text has its own narrative time, marked out sequentially by the section numbers. It also refers to the serial time of the computation, and to the "parallel time" of certain "auxilary variables" which evolve in lockstep with the main variables of the program. On top of this, the reader is constantly aware of the way the program loops back on itself, providing a structure for WEB to reorder all the code as the PASCAL compiler demands. And then there is the overall evolution of the algorithm as a process when the program is run. Knuth's program has the complex temporality of a Virginia Woolf novel, and a Woolfian quality of internal reflection. Perhaps for someone whose daily life is number theory, the program would also have those Woolfian qualities of sacredness and care that we were, for the most part, unable to draw from the text.

We also discuss the personality of the text. Knuth argues from the start that "[p]rogramming is a very personal activity," and suggests that the programmer's personality should shine through the code. If you can see the person behind the code, you can understanding the reasoning behind the code, and therefore can understand the code itself. One member of the group suggested that this contradicts the common ideal of "[egoless programming](https://blog.codinghorror.com/the-ten-commandments-of-egoless-programming/)," which is important for engineers working on complex projects in large teams over many years. How "egotistical" is Knuth's idea of "personality"? Knuth himself is a master-craftsman. Perhaps for him there is no link between personality and ego, for the master-craftsman loses herself in the craft, and can bear any criticism of her work so long as it is in the cause of programming elegance. But perhaps ego and personality cannot so easily be separated.

We recommence next week in the fourth paragraph of **D. How the example was specified**.
