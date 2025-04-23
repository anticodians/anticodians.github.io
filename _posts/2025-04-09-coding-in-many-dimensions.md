---
layout: post
title: "Coding in Many Dimensions"
summary: We meet the tensor
---

This week we read up to page 41 of *The Little Learner*, and "learned" a bit about the tensor, the "[fundamental data structure in deep learning](https://docs.racket-lang.org/malt/overview.html?q=struct#%28part._overview-tensors%29)".

## Kurzgesagt

In a nutshell, a tensor is a *multidimensional array*. You can have one-dimensional tensors (also called vectors):

$$
\begin{Bmatrix}
1.0 & 27.1 & x^2 & -0.7 \\
\end{Bmatrix}
$$

You can have two-dimensional tensors (also called matrices):

$$
\begin{Bmatrix}
42 & 42 & 42 \\ 42 & y & 42 \\ 42 & 42 & 42 \\
\end{Bmatrix}
$$

You can have three-dimensional tensors. This tensor could represent a (very small) bitmap image, with four pixels, each of which has a colour specified by three values for red, green and blue:

$$
\begin{Bmatrix}
\begin{Bmatrix}7 \\ 3 \\ 255\end{Bmatrix} & \begin{Bmatrix}62 \\ 107 \\ 7\end{Bmatrix} \\ \begin{Bmatrix}200 \\ 200 \\ 100\end{Bmatrix} & \begin{Bmatrix}62 \\ 34 \\ 254\end{Bmatrix} \\
\end{Bmatrix}
$$

Each of the numbers in a tensor is called a *scalar*. Presumably this name comes about because of the way *scalar multiplication* works. If you multiply a tensor by a single number, then you simply multiply all the members of the tensor by that number:

$$
\begin{Bmatrix}
42 & 42 & 42 \\ 42 & y & 42 \\ 42 & 42 & 42 \\
\end{Bmatrix} \times 6 = \begin{Bmatrix} 42 \times 6 & 42 \times 6 & 42 \times 6 \\ 42 \times 6 & y \times 6 & 42 \times 6 \\ 42 \times 6& 42 \times 6 & 42 \times 6 \\
\end{Bmatrix}
$$

Thus the number $6$ "scales" the tensor, and can be called a *scalar*.

(I have just read [the relevant Wikipedia page](https://en.wikipedia.org/wiki/Scalar_(mathematics)) to verify my conjecture about the etymology of "scalar," and I'm not totally wrong. The term originally derives from the Latin for "ladder.")

(The derivation of terms in linear algebra is always interesting. As mentioned above, a two-dimensional tensor is normally called a "matrix." Believe it or not, this word derives from the Latin for "womb"!)

Scheme doesn't natively support tensors. It only natively supports one-dimensional arrays. The [malt package](https://docs.racket-lang.org/malt/index.html?q=struct) devised for *The Little Learner* adds in support for tensor operations. The key rule of tensors is that they need to have a consistent shape. This is not a valid tensor, for example:

$$
\begin{Bmatrix}
1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 &  & 9 \\ 10 & & 
\end{Bmatrix}
$$

The "second" or "outer" dimension is okay: there are three columns. But the "first" or "inner" dimension is no good: each column has a different number of rows:

$$
\begin{Bmatrix}
1 \\ 4 \\ 7 \\ 10
\end{Bmatrix}
\begin{Bmatrix}
2 \\ 5
\end{Bmatrix}
\begin{Bmatrix}
3 \\ 6 \\ 9 
\end{Bmatrix}
$$

The malt package enforces this rule. If you try to create this faulty tensor with mismatched columns, you will get an error:

```scheme
(tensor (tensor 1 4 7 10)
        (tensor 2 5)
        (tensor 3 6 9))

; tensor: Mismatched shapes: (#(1 4 7 10) #(2 5) #(3 6 9))
```

## Some functions

We learned a few useful `malt` functions in the first part of the chapter.

- [`scalar?`](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): is this object a scalar?
- [`tensor?`](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): is this object a tensor?
- [`shape`](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): what is the shape of this tensor? How many *rows*, *columns*, *aisles* etc. does it have? What is the length of each of its dimensions? For example, if you have a full-colour bitmap image in 1800 x 1169 resolution, and asked for `(shape my-big-image)`, you would get `'(1800 1169 3)` as the answer: 1800 *columns*, 1169 *rows* and 3 *colour values*.
- [`tlen`](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): what is the size of the outer dimension of this tensor? E.g. if you have a matrix with 6 columns and 3 rows, the `tlen` of the matrix will be `6`. You can use `tlen` to implement the `shape` function.
- [`rank`](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): how many dimensions a tensor has. For instance, your typical spreadsheet is a two-dimensional tensor, made up of *rows* and *columns*. If you had your spreadsheet inside a Racket program, and typed `(rank my-spreadsheet)`, out would pop the answer `2`.
- [tref](https://docs.racket-lang.org/malt/Tensor_functions.html?q=struct#(part._.Tensor_functions)): how to get items out of a tensor. For instance, if you wanted the third column of a tensor called `my-spreadsheet`, you could write `(tref my-spreadsheet 2)`.

## Our upward course...

Sometimes scalars and tensors can be hard to tell apart. For example, here is a scalar:

$$ 
6
$$

In Scheme/Racket, that would be:

```scheme
6
```

Here is a one-tensor:

$$
\begin{Bmatrix}6\end{Bmatrix}
$$

Or in Scheme/Racket:

```scheme
(tensor 6)
```

Now here is a two-tensor, or matrix, with one row and one column:

$$
\begin{Bmatrix}\begin{Bmatrix}6\end{Bmatrix}\end{Bmatrix}
$$

```scheme
(tensor (tensor 6))
```

And a three-tensor...

$$
\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}6\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}
$$

```scheme
(tensor (tensor (tensor 6)))
```

And a four-tensor...

$$
\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}6\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}
$$

```scheme
(tensor (tensor (tensor (tensor 6))))
```

And a five-tensor...

$$
\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}\begin{Bmatrix}6\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}\end{Bmatrix}
$$

```scheme
(tensor (tensor (tensor (tensor (tensor 6)))))
```

What is a dimension anyway? We may leave the last words to [A. Square](https://www.gutenberg.org/files/201/201-h/201-h.htm):

> And once there, shall we stay our upward course? In that blessed region of Four Dimensions, shall we linger on the threshold of the Fifth, and not enter therein? Ah, no! Let us rather resolve that our ambition shall soar with our corporal ascent. Then, yielding to our intellectual onset, the gates of the Sixth Dimension shall fly open; after that a Seventh, and then an Eighth— How long I should have continued I know not. In vain did the Sphere, in his voice of thunder, reiterate his command of silence, and threaten me with the direst penalties if I persisted. Nothing could stem the flood of my ecstatic aspirations.