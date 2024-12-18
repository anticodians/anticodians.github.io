---
layout: post
title: The End of Literate Programming
summary: We finish Knuth's essay. What's next?
---

## The end of the affair

At our final meeting for 2024, we completed reading Knuth's *Literate Programming*. In the final section, Knuth considers "Retrospects and Prospects" for literate programming. In this section, Knuth is explicit about who literate programming is for: computer scientists and systems programmers, rather than hobbyists. This context justifies many of Knuth's arguments throughout the essay, about the kinds of literacy assumed by the `WEB` system. But it also widens the main gap in his philosophy—the gap between the programmer and the reader. He anticipates the programs will become works of literature, which implies a wide readership, but he restricts `WEB` to a small subset of people, resulting in a restricted writership. In this way Knuth sharpens the *literary* aspect of his enterprise, for indeed literature too is written by the few for the many to consume.

With that, our first major reading for the group came to an end.

## After the end

We spent some time looking at the upshot of Knuth's new programming system. On his website, he has [published many literate programs](https://www-cs-faculty.stanford.edu/~knuth/programs.html), in addition to publishing three books written in either `WEB` or `CWEB`, which contain the programs for [TeX](https://dl.acm.org/doi/book/10.5555/536123), [Metafont](https://dl.acm.org/doi/book/10.5555/536126) and [the MMIX virtual machine](https://link.springer.com/book/10.1007/3-540-46611-8).

Literate programming has inspired many programming systems, but not in the manner Knuth proposed. He saw `WEB` as a system for highly skilled programmers to write complex software systems. But `WEB` (and its descendent `CWEB`) have not found much use in this domain. Instead, programming language designers have designed ever more capable documentation-generation systems, which allow software to be composed in a more conventional format, but with excellent computer-generated documentation. Python includes [pydoc](https://docs.python.org/3/library/pydoc.html) as part of its standard library, for example, while Rust ships with [rustdoc](https://doc.rust-lang.org/rustdoc/index.html). Such tools allow a developer to include documentation in their code, and generate attractive websites for their software. They do not support the creation of elegant books of the kind that Knuth prefers, and in particular, do not free the programmer from the sytax of their chosen programming language.

The Knuthian ideal of literate programming has caught on in a different community: data science. Statisticians, digital humanists, data analysts, lab scientists and others frequently use tools such as [EMACS org-mode](https://orgmode.org/worg/org-contrib/babel/), [RMarkdown](https://rmarkdown.rstudio.com/) and [Juypter Notebooks](https://jupyter.org/) to write their software. This form of literate programming is nonetheless distinct from Knuth's. Knuth foresaw systems programmers building complex reusable systems using literate tools. Data scientists tend to write more ephemeral, simple programs, which analyse a particular dataset or form the basis for a particular article or report. When a data scientist *does* take the time to develop a more complex and reusable piece of software, they are more likely to do so in the form of a simple R, Python or Julia package. While it is possible to write such software in a more literate style using tools such as [nbdev](https://nbdev.fast.ai/), this is not a common practice.

It is a pity that Knuth's vision of programming-as-literature has not gone mainsteam. Source code is the primary medium of communication for millions of people who work every day as programmers. They write software that affects all of us, and if this software were readable by the general public, then the systems that govern our lives could in principle be more open and democratic. Even an experienced programmer can find it difficult to find a reading path through a complex program. If essential pieces of software such as [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) (i.e. Wikipedia), [TensorFlow](https://tensorflow.org/) or [Bluesky](https://github.com/bluesky-social/social-app) were written and published in a Knuthian style with a linear narrative, then more people might be inclined to read and debate the code.

## What next?

We will reconvene in February 2025, as the summer recess draws to a close here in Australia. Stay tuned for our next reading, which will involve the source code of a Large Language Model. Tell then, Happy Holidays!