---
layout: post
title: Beginning How To Prove It
tags: how-to-prove-it
---

I just finished working through the introduction of [How To Prove It][1]. The book presents a structured approach to reading and writing proofs, that is analogous to how we compose elements like `if-then` statements and `do-while` loops to write computer programs. I'm personally finding the book very promising, and highly recommend working through the introduction to get a taste of the kind of mental process this provokes.

*Aside*: I think the books that make the most impact on me are the ones with carefully designed exercises that really test how thorough you believe you are. This also goes to show that I really rely on exercises to force deep reading; another `FIXME` item for my flawed reading habits.

It looks like the only solutions and discussions on this book are over at [Himanshu Gupta's blog][2]; I've found some real gems in the comment discussions there, so they're now mandatory post-exercise readings for me.

## Notes

Below are my notes while working through the introductory exercise:

### Question 1

This questions builds on conjecture 2,

> If n is not prime, then $$ 2^n - 1 $$ is not prime.

and its corresponding proof, which shows us how to construct the factors $$ x $$ and $$ y $$ of $$ 2^n - 1 $$ from the factors $$ a $$ and $$ b $$ of $$ n $$.

*a. Factor $$ 2^{15} - 1 = 32,767 $$ into a product of two smaller positive integers.*

$$
\begin{align*}
   &n = 15 \implies a = 5, b = 3\\
   \\
   &x = 2^b - 1 = 31\\
   &y = 1 + 2^b + 2^{2b} = 1057\\
   \\
   &2^{15} - 1 = 31\times1057
\end{align*}
$$

*b. Find an integer $$ x $$ such that $$ 1 < x < 2^{32767} - 1 $$ and $$ x $$ divides $$ 2^{32767} - 1 $$.*

This is equivalent to stating that $$ 2^{32767} - 1 = xy $$, where $$ 1 < y < 2^{32767} - 1 $$. Let $$ 2^{32767} - 1 = 2^n - 1 $$. Then,

$$
\begin{align*}
  n &= 32767\\
    &= 1057\times31\\
    &= a \times b\\
  \\
  \implies a &= 1057\\
           b &= 31\\
  \\
  2^{32767} - 1
    &= x \times y\\
    &= (2^b - 1)(1 + 2^b + 2^2b + ...)\\
  \\
  \implies x &= 2^b - 1\\
             &= 2^{31} - 1\\
             &= 2147483647
\end{align*}
$$

### Question 2

*Make some conjecture about the values of $$ n $$ for which $$ 3^n - 1 $$ is prime or $$ 3^n - 2^n $$ is prime.*

Let's make a table.

<div class="table-wrapper">

n  |  $$3^n - 1$$ |  $$3^n - 2^n$$  |  n prime?  |  $$3^n -1$$ prime?  |  $$3^n - 2^n$$ prime?
:- | :-           | :-              | :-:        | :-:                 |  :-:
1  |  2           |     1           |      N     |      Y              |        N
2  |  8           |     5           |      Y     |      N              |        Y
3  |  26          |     19          |      Y     |      N              |        Y
4  |  80          |     65          |      N     |      N              |        N
5  |  242         |     211         |      Y     |      N              |        Y
6  |  728         |     665         |      N     |      N              |        N
7  |  2186        |     2059        |      Y     |      N              |        Y

</div>

Conjectures:

   1. If $$ n $$ is prime, then $$ 3^n - 2^n $$ is prime.
   2. If $$ n $$ is not prime, then $$ 3^n - 2^n $$ is not prime.
   3. If $$ n > 1 $$, then $$ 3^n -1 $$ is not prime.

### Question 3

*The proof of theorem 3 gives a method of finding a prime number different from any in a given list of prime numbers*

   * *Use this method to find a prime number different from 2, 3, 5 and 7.*
   * *Use this method to find a prime number different from 2, 5 and 11.*

Theorem 3 proves that there is an infinite number of primes using 2 cases.

Given a list of primes $$ p_{1}, ..., p_{n} $$, if $$ m = p_{1} \times p_{2} \times ... \times p_{n} + 1 $$, either:

   * $$ m $$ is prime, and is hence not in the finite list $$ p_{1}, ... p_{n} $$, or
   * $$ m $$ is a product of primes $$ p $$ and $$ q $$. Since $$ m $$ is not divisible by $$ p_{1}, p_{2}, ..., p_{n} $$, $$ p $$ or $$ q $$ are not in the finite list $$ p_{1}, ..., p_{n} $$.

So we have 2 ways of finding a prime that is not in the given list of primes:

   * $$ m = p_{1} \times p_{2} \times ... \times p_{n} + 1 $$, and $$ m $$ is prime, so it is the prime we need.
   * $$ m = p \times q $$, and $$ m $$ is not prime, so $$ p $$ and $$ q $$ are the primes we need.

Using this, we have:

   * $$ 2 \times 3 \times 5 \times 7 + 1 = 211 $$, 211 is a prime not in the list.
   * $$ 2 \times 5 \times 11 + 1 = 111 = 3 \times 37 $$, 3 and 37 are primes not in the list.

The comments in [Himanshu's blog][1] brought forth an interesting related conjecture; if $$ p_{1}, p_{2}, ... $$ are primes, then is $$ p_{1} \times p_{2} \times ... \times p_{n} + 1 $$ always prime?

The numbers of the form $$ p_{1} \times p_{2} \times ... \times p_{n} + 1 $$ are called *Euclid numbers*. The conjecture is false, as seen in the counter-example of the [first composite Euclid number][3].

### Question 4

*Find 5 consecutive integers that are not prime.*

This is a direct application of the theorem 4.

$$
\begin{align*}
  n &= 5\\
  x &= (5 + 1)! + 2\\
    &= 6! + 2\\
    &= 722
\end{align*}
$$

Required sequence: 722, 723, 724, 725, 726

### Question 5

*Use the table in figure 1 and the discussions on p.5 to find two more perfect numbers.*

This is a direct application of the theorem proven by Euler,

> If $$ 2^n - 1 $$ is prime, then $$ 2^{n-1} \times (2^{n} - 1) $$ is perfect.

Using this theorem, we have the following:

$$
\begin{align*}
  n &= 5\\
\implies 2^4 &\times (2^5 - 1)\\
    &= 16 \times 31\\
    &= 496\\
    &= 1 + 2 + 4 + 8 + 16 + 31 + 62 + 124 + 248\\
  \\
  n &= 7\\
\implies 2^6 &\times (2^7 - 1) = 8128
\end{align*}
$$

### Question 6

*The sequence 3, 5, 7 is a list of three prime numbers such that each pair of adjacent numbers in the list differ by 2. Are there any more such "triplet primes"?*

Such a triplet can only occur among a triplet of odd numbers (since 2 is the only even prime number).

Among consecutive odd numbers, apart from 2, 3, 5 and 3, 5, 7, there is no such triplet. Every third odd number greater than 15 is a multiple of 3, so we can never get a sequence of 3 odd numbers such that they are all prime; at least one of them will have 3 as a factor.

[1]: http://www.cambridge.org/us/academic/subjects/mathematics/logic-categories-and-sets/how-prove-it-structured-approach-2nd-edition
[2]: http://technotes-himanshu.blogspot.in/search/label/htpi
[3]: http://en.wikipedia.org/wiki/Euclid_number
