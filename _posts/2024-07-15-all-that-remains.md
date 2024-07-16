---
layout: post
title: All that remains
summary: The table is empty, now to fill it!
---

## The three-act structure of the literate program

>The remaining task is to fill table *p* with the correct prime numbers.

Halfway through Knuth's program, we find the algorithm for generating primes. To this point, his program has focussed on controlling the machine. He has defined the global parameters for the program, and some complicated routines for placing numbers in a printed table. Thus far, we have read about variables such as *row_offset*, being the number of rows that have already been printed, and constants such as *cc*, the number of columns that can be accomodated on a single page of the table.

In the group, we spoke about the relationship between the programmer and the machine. In Digital Humanities, we only rarely interact with the machine in this direct and geometric way. Gone is the age of the early microcomputer, when the computer in 'text mode' would allow the user to display a certain number of characters on a screen of fixed column and row dimensions. Today we take flowing text for granted. Gone also are the days when printing a simple heading at the top of each page would require six statements:

```
begin print_string(`The First `);
print_integer(m);
print_string(` Prime Numbers --- Page `);
print_integer(page_number); new_line; new_line;
```

In Python, this could be accomplished with string interpolation:

```{python}
print(f"The First {m} Prime Numbers --- Page {page_number}\n")
```

To complicate things, Knuth's heading-printing code is actually written using a series of macros defined in a previous section. When the macros are applied, the resulting PASCAL code is as follows (see Figure 3 in Knuth's text):

```
WRITE('The First '):WRITE(M:1);
WRITE(' Prime Numbers --- Page ');
WRITE(PAGENUMBER:1);WRITELN;WRITELN;
```

Only after several pages of this complicated programming does Knuth arrive at the 'task' of actually generating the first *m* prime numbers, which would seem to be the point of the program. Although of course, generating the first *m* primes is *not* the point of this program. The point of this program is to illustrate the concept of 'literate programming' and to demonstrate the WEB system. The inner purpose, to generate the first *m* primes, is a fictional purpose. Knuth is telling a story about a fictional version of himself, who needs to generate the primes, and wishes to write a readable program for doing so.

In this context, his heading code is very good. It gives him scope to demonstrate WEB's macro system. It gives him scope to interleave code and explanation. It gives him scope to reflect on the proper narrative flow of a literate program.

In Knuth's view, the program should have a three-act structure. Act 1, declare the basics. Act 2, do the housekeeping. Act 3, implement the algorithm. He is a [Shandyan](https://en.wikipedia.org/wiki/The_Life_and_Opinions_of_Tristram_Shandy,_Gentleman) narrator, who includes many digressions—e.g. how to print a heading—on the way towards his ultimate goal. The digressions have caused some level of frustration in our group, but perhaps this is the point. Act 2 creates suspense. Knuth establishes the fictional purpose of his program in the first block of code, and then waylays the reader, whetting their appetite for the 'real' programming to come. It was some relief in our group to finally reach section 11, when the 'remaining task' of generating the primes  recurred. Act 3 begins with a bang.

In this article, the programmer is like an eighteenth-century stage manager. The script of the play is only secondary. What matters is the scenery, the special effects, the footlights and the songs. We watch the play from the wings, as the stage manager summons up the mechanisms of the theatre. Flood the stage! Bring on the horses! Swing in the heroine on the trapeze! Knuth is a poet-hacker of the old school, the plot of whose text is the unfolding of the machine. In his hands, the abstract purity of Djikstra's algorithm for finding the primes becomes concrete. As one in the group said: you can't have a table of numbers if you haven't got a way of printing the table. Knuth may well agree.

## Conventions

```
〈 Output a line of answers 8 〉≡
  begin for c ← 0 to c - 1 do
    if row_offset + c * rr ≤ m then
      print_entry(p[row_offset + c * rr]);
  new_line;
  end
```

A second theme of our discussion this week was literary convention. Few in the group find Knuth's naming conventions easy to understand. Knuth likes his code to look like algebra, and uses a host of unstated convention when he names variables. To someone with a background in discrete mathematics, it must seem obvious that `n` is how many primes we currently have, and `m` is the maximum number we'd like to reach. It must seem normal that `j` is the current number we are testing, and `k` is the index of the current prime number in the table. It must seem normal too that `r`, `c`, and `w` mean the current row, column and word position, while `rr`, `cc` and `ww` mean the maximum number of rows, columns and word positions. But in our group we don't all have this background, and these choices of name are not so obvious!

Many in the group would maybe have preferred the above code if it looked like this:

```
〈 Output a line of answers 8 〉≡
  begin for column ← 0 to column - 1 do
    current_prime_index ← row_offset + column + num_rows;
    if current_prime_index ≤ max_number_of_primes then
      print_entry(primes[current_prime_index]);
  new_line;
  end
```

Most of us have done most of our coding in Python, where it is common to label variables explicitly as above. Indeed, [pylint](https://pylint.readthedocs.io/en/latest/) will highlight single-letter variable names like `c` or `r`, recommending the coder to expand them. Most of us do our coding in a humanistic context, where algebra is an uncommon acquirement. Mathematical formulae tend to look forbidding rather than familiar, even in *Digital* Humanities.

This is all to say that conventions are strong in coding as well as in other kinds of writing. These conventions are generally used unconsciously: even Knuth, the most self-aware of programmers in this most self-aware program, doesn't note the algebraism of his own style!