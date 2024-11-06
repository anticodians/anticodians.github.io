---
layout: post
title: Psychological correctness
summary: Knuth's aesthetic theory of cognition
---

In this meeting, we read the crucial section of "Literate Programming," `J`, in which Knuth lays out his theory of 'programs as webs'. This section justifies `WEB` in the most general possible terms: all programs are already webs, Knuth argues. All `WEB` does is allow the programmer to clearly express the structure that is already there.

Knuth uses the 'web' metaphor in an interesting way. Those of us who are used to the Internet and the World Wide Web may think of a 'web' as an inherently dynamic or unstable system. We browse or surf the web. We hop from page to page, from app to app, using hyperlinks. We summon up fragments of the web using search engines, or allow recommendation algorithms to summon up fragments for us as we scroll the feeds of our favourite platforms.

This is not what Knuth means by web. For Knuth, a web is a static, well-ordered structure, like the delicately woven web of a spider, or a narrative tapestry whose threads are chronological. A web is for reading from start to finish. A web has a finite set of components, which have been joined carefully by the weaver of the web. Of course, you may use an index to jump to particular joins on the web. You may use cross references to travel along particular strands. But the web itself is single and entire, with a beginning, middle and end.

## Structures and structures

> A hierarchical structure is present, but the most important thing about a program is its structural relationships. (p. 107)

Knuth argues `WEB` accomodates both 'top-down' and 'bottom-up' programming, or rather, it transcends these two approaches. The `WEB` programmer can start with a top-level description of a program, or they can start by defining subroutines, or they can mix both freely. This freedom to decide between top and bottom at will frees the programmer from the 'hierarchy' of the program. Of course, in the end, '\[a\] hierarchical structure is present': a program must be a single object the computer can execute, comprising smaller parts that lie within it. But the `WEB` approach allows the programmer to reveal the 'structural relationships' of the program: the logical and intellectual links between different parts of the program.

For example, perhaps some global variables are manipulated by subroutine X, and others are manipulated by subroutine Y. From a hierarchical perspective, each global variable and each subroutine is a separate part of the program, on the same level, while the code inside each subroutine is at the next level down, nested within the subroutine. Using `WEB`, however, the programmer can explicitly reveal the relationships between the variables and the subroutines, for example by declaring the variables next to the subroutines that matter to them, or by building up the subroutines in parts that a clearly related to other global aspects of the program.

There is an interesting slippage in Knuth's argument. There is the 'hierarchical structure' on the one hand, and the 'structural relationships' on the other. Both of these are 'structur(e|al)'. What makes them different? How are they related?

Knuth implies that there is no single description of a program that is the right one. Programs have many parts, which combine to form the entire program. These parts have many possible relationships: the orderly hierarchy of their execution by the machine is only one set of relationships. The human reader of a program may observe many other sets of relationships in the program that matter to them.

We could think of this in practical terms. A human might use a profiler, observing how and when different parts of the program are called in practice. They might use a flowchart tool to visualise the control flow. They might write out mathematical theorems that characterise the invariants of parts of the program. They might observe the way that the program models the problem domain, the user, the machine itself. There are (possibly) infinitely many 'structures' in a program. Knuth's aim with `WEB` is to let the programmer structure their program in whatever way will maximise human comprehension of the code.

## Psychological correctness vs. \[personal\] style

Knuth's theory of coding style is simulataneously *aesthetic*,  *cognitive* and *functional*. Code written in `WEB` should be aesthetically pleasing, according to literary criteria; it should be easily comprehended (or congnised); and it should function correctly.

These three aims don't always go together, according to Knuth. He gives an example on page 108. Imagine a programmer is writing a function that does a simple data update, but it needs to check the user input for errors. If the programming language obliges the programmer to put the error-checking code first, then they may feel the urge to shrink the error-checking. The error-checking code is tangential to the function: what really matters is the code at the end, which actually performs the data update for which the function is being written. If there are dozens of lines of error-checking code, which make up virtually the whole function, the programmer may find the function aesthetically repulsive. It would be like designing a pencil with a grip so enormous and contorted that you can no longer clearly see the barrel and tip of the pencil itself. In this case, *aesthetics* pulls against both *cognition* and *functionality*. To make the function seem less ugly, the programmer will try to write the error-checking code as concisely as possible, which may mean it is terse and difficult to understand. They will also be tempting to omit error checks, potentially impairing the functionality of the code.

Knuth demonstrates how `WEB` resolves the contradiction between *aesthetics*, *cognition* and *functionality*. By giving the programmer complete control over the presentation of the code, and the ability to add labels or commentaries to any part of it freely, `WEB` allows the programmer to achieve any *functionality* they like without compromising on either *aesthetics* or *cognition*.

There is a tight link, and nonetheless a tension between aesthetics and cognition in Knuth's theory. Knuth argues that the best way to present a program is in the "psychologically correct" order. But he also argues that programmers can and should develop a personal "style" of programming. If there is a "correct" way to present the program, how is there room for individual "style"?

Knuth's theory of "psychological correctness" is highly individualised. He argues that a program should represent the programmer's "stream of consciousness" (p. 107)—that is, the program should be written in the order that the programmer conceived of it. He insists throughout the essay that in his own experience, he only ever envisages a program in one order. There is an order in which the program occurred to him, and this is the order in which it must be written. He argues that when he reads another programmer's code, he can understand their stream of consciousness easily: the program he presents on pages 98-102 of the article is actually no Knuth's own stream of consciousness, but Edsger Dijkstra's.

There is a commonsense aspect to this. If the programmer builds up the program logically, then they can communicate this logical process to the reader, who will hopefully find it easer to comprehend what is going on. Knuth does occasionally modify his theory, admitting that the programmer should simply regurgitate their actual "stream of consciousness," but shape the program text with the reader in mind.

But Knuth nonetheless presents the idea of "psychological correctness" in such a stark way that its implications are thriling and extreme. Is it true that every program Knuth writes appears to him in exactly one way? Is this a universal experience of programming? We felt in the group that perhaps Knuth is not accounting for his own extreme level of skill and learning—most programmers probably fumble around, and need to experiment, much more than this most famous computer programmer needs to when he writes software. Is it true that we can understand one another's thought-processes so easily? Many in our group found the presentation of the primes program on pages 98-102 extremely difficult to follow. The program makes many assumptions about the prior knowledge and discursive competence of its readers. Does Knuth believe that there is a single programming literacy that all programmers share, such that the reader of any program can be assumed to be the same kind of person with the same kind of consciousness?

There is something deeply Kantian about Knuth's views. He seems to believe in a universal rationality, which extends to the task of aesthetic judgment, and which links cognition to the feeling of beauty. As an unreconstructed Romantic, I find this point of view to be very attractive, even if our experience in this very group demonstrates (for the millionth time) that rationality is more contingent and culturally determined that Kantians may like to admit.

We recommence next time partway through section `K`, on page 108.