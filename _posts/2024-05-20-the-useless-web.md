---
layout: post
title: The useless web?
summary: Knuth's WEB is certainly beautiful. Is it useful?
---

We continue our reading of [Literate Programming](https://academic.oup.com/comjnl/article-pdf/27/2/97/981657/270097.pdf), by Donald Knuth.

We completed up to section 2 of Knuth's web program to print the first *n* prime numbers. Having encountered the program definition, we have in some sense read the entire thing.

We did discuss whether modern code editors render Knuth's entire notion of the 'web of code' otiose. We in particular considered EMACS, a code editor that was becoming popular at the time the paper was written.

EMACS stands for “editor macros,” and it basically allows a coder to write little programs that let them interact with their source code. The particular thing I was thinking of is the way you can use EMACS or similar programs to navigate your codebase. Say you come across a function called “check_if_prime” and you don’t know how it works. In EMACS you should be able to hit a keyboard shortcut, and be taken to the part of the source code where “check_if_prime” is defined, so you can see what it does. You should then be able to hit another keyboard shortcut to go back to where you were.
 
If you have a good code editor, is all the elaborate cross-referencing of a WEB program required?
