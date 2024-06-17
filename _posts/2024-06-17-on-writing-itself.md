---
layout: post
title: On Writing Itself
summary: When code 'writes itself', what is written, and who exactly writes it?
---

>Now that appropriate auxiliary variables have been introduced, the process of outputting table *p* almost writes itself.

What does it mean for code to 'write itself'. On a commonsensical level, it is obvious what Knuth means. When appropriate variables have been defined, then it is plain how they should be combined to express the programmer's intent. Knuth effectively makes a prediction: any programmer worth their salt could see how the next part of the code should be written. As one of our members observed, however, lurking beneath this commonsensical supposition is a host of metaphysical presuppositions. What makes the code obvious? Why does the writer feel that the code has become autonomous, and is running off in its own direction?

There are many different agents in the 'assemblage' of the WEB system as Knuth writes. The PASCAL language, with its grammar and vocabulary. The WEB system itself, with its various (rather quirky) affordances. The presumed reader of the *Computer Journal* for whom is code is really being written. The logical force of mathematics and the algorithm. The beauty of the program, which is put there by the programmer but then turns back on its creator to bewitch their senses. When the the 'code writes itself', it is really some combination of these forces acting together to educe the code.

What code? This code:

```
〈 Print table p 8 〉≡
    begin page_number ← 1; page_offset ← 1;
    while page_offset ≤ m do
        begin 〈 Output a page of answers 9 〉;
        page_number ← page_number + 1;
        page_offset ← page_offset + cc * rr;
        end;
    end;
```

The code that has 'written itself' has offloaded its job to another part of the program! The actual code that 'writes itself' is essentially just a piece of housekeeping that keeps track of which page we're up to in the printing loop. We discussed for some time Knuth's decision to leave the actual outputting of a 'page of numbers' to another part of the program. No doubt his judgement is good. He strives for a certain kind of modularity, where each module is highly concrete and can be summed up in a verb phrase ("Output a page of answers").

Reading the code again, it does have a feature I find disquieting. Presumably `〈 Output a page of answers 9 〉` uses some of the variables we have already encountered, including `page_offset`, but the way this code is written, you have no idea which variables will be used or altered by `〈 Output a page of answers 9 〉`. Is this a deficiency of PASCAL, or of Knuth's code, or of WEB itself? Pascal supports subroutines with named parameters (at least, it does so today). Why not write a subroutine here that explicitly shows in its signature which variables will be usd to `〈 Output a page of answers 9 〉`?

This raises the additional question of 'readability'. This is one of the major aesthetic criteria of modern programming, but what it means is debatable. Knuth argues that his code above is readable because it clearly states the programmer's intention, and states it in (roughly) the order that the programmer thought up their intention. But from another perspective, the code above is not especially 'readable' because it doesn't clearly indicate the flow of data through different parts of the program.

Knuth's judgments about what to include, exclude, abstract or concretise are in every case fascinating. As another member noted, he seems to strive for 'modularity' in all aspects of the WEB code, even the prose components, which are carefully fenced off into discrete modules by square brackets and section numbers.

We resume next session at section 9 of his program for printing the first 1000 prime numbers.