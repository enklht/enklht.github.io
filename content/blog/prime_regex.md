+++
title = "The Prime Detecting Regex And Why It Is Not a Regex"
date = 2025-10-04
updated = 2025-10-04
[taxonomies]
tags = ["Computer Science"]
+++

You may have come across this regular expression that detects prime numbers:

```perl
^.?$|^(..+?)\1+$
```

While this pattern appears to work, there's a mathematical proof that shows why true regular expressions cannot detect prime numbers.
Let's dive into how this pattern works and why it's not actually a regular expression in the mathematical sense.

## How Does the Pattern Work?

This regex attempts to identify non-prime numbers using a clever backtracking mechanism.
(For an in-depth technical analysis, check out [Ilya's excellent article](https://illya.sh/the-codeumentary-blog/regular-expression-check-if-number-is-prime/))

For an input string of length $n$, the pattern works in two parts:

1. `^.?$` matches strings of length 0 or 1, which are non-prime by definition
2. `^(..+?)\1+$` tries to find divisors:

- `(..+?)` captures a group of dots (length $k$)
- `\1+$` attempts to match that same pattern repeatedly

The magic happens through backtracking: when testing a number $n$, the regex engine tries different values of $k$ until either:

- It successfully finds a $k$ that divides $n$ evenly (proving the number is composite)
- It fails to find any such $k$ (indicating the number is prime)

## Understanding Regular Languages

To understand why this pattern isn't a true regular expression, we need to look at what makes a language "regular" in computer science theory.

A regular language is traditionally defined as one that can be recognized by a finite automaton.
However, we can also understand it through its constructive definition.

Given an alphabet $\Sigma$, regular languages are built using these simple rules:

1. Basic building blocks:
    - Empty language $\emptyset$ is regular
    - Empty string language $\set{\epsilon}$ is regular
    - Single-character languages $\set{a}$ for any $a \in \Sigma$ are regular
2. Combination rules:
    - Concatenation: If $R_1$ and $R_2$ are regular, then $R_1 \cdot R_2 := \set{ u \cdot v; u \in R_1, v \in R_2 }$ is regular
    - Union: If $R_1$ and $R_2$ are regular, then $R_1 \cup R_2$ is regular
    - Kleene star: If $R$ is regular, then $R^* := \set{ w^i; w \in R, i \ge 0 }$ is regular

These rules directly correspond to the basic operations in traditional regular expressions:

- Concatenation: writing patterns next to each other
- Union: the | operator
- Kleene star: the * operator

## Why Prime Numbers Can't Be Regular: The Pumping Lemma

We can prove that prime numbers cannot be described by a regular language using the Pumping Lemma.
This fundamental theorem states that all regular languages have a repeating property that prime numbers lack.

Specifically, the Pumping Lemma says that for any regular language $L$, there's a number $p > 0$ (called the pumping length) where any string $s \in L$ longer than $p$ can be split into three parts $s = xyz$ such that:

1. $|xy| \leq p$
2. $|y| > 0$
3. $xy^iz \in L$ for all $i \geq 0$

The name "pumping" comes from the idea that you can "pump up" the middle part ($y$) by repeating it any number of times, and the resulting string must still be in the language.
This property emerges from how finite automata work: when processing a long enough string, they must eventually revisit a state they've seen before, creating a cycle that can be repeated.

### Proof by Contradiction

Here's why the language of prime numbers violate this property:

1. Let's assume prime numbers form a regular language $L = \set{1^n; n \text{ is prime}}$
2. Take the pumping length $p$
3. Choose a prime number $q$ larger than $p$ and consider $s = 1^q$
4. By the Pumping Lemma, we can split $s$ into $xyz$ where:
    - $|xy| \leq p$
    - $|y| > 0$
    - $xy^iz$ should be in $L$ for all $i \geq 0$ (\*)
5. Let $k = |y|$.
When we pump the string:
    - With $i$ pumps, we get a string of length $q - k + ki$.
    - Set $i := q+1$, then the length is $q - k + k (q+1) = q(k+1)$.
    - This number is composite (it's $q$ times $(k+1)$)
    - Therefore, it can't be in our language of prime numbers, but it contradicts (\*)

This contradiction proves that prime numbers cannot form a regular language.

## The Real Story Behind the Pattern

So why does our original pattern work? The answer lies in modern regex engines like Perl's, which go far beyond traditional regular expressions.
These engines include features like:

- Backreferences (like `\1`)
- Look-ahead and look-behind assertions

These additions give modern regex engines the power to recognize some context-sensitive languages, far surpassing the capabilities of true regular expressions.
This explains why the prime-detecting pattern works in Perl but not in basic tools that implement strict regular expressions.
