---
title: 'How do spellcheckers work?'
description: 'How do spellcheckers work?'
pubDate: 'Feb 28 2025'
heroImage: '/28022025/banner.png'
---

We all know those wiggly red lines that show up under misspelled words—a small but helpful feature we don’t often think about. It uses a smart system to keep our writing clear. When our team received an intriguing request from the business to implement a spellchecker, it truly captured my attention in a way I never anticipated. Yup... I could've just used an api that does the spellchecking for me, but I was more interested in how things work behind the scene, so this led me to investigating how spellcheckers work.

let's take a look at the timeline


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/16jlhnn01b9gdz0vpf4s.png)

## late 1950s and early 1960s

The idea for spellcheckers started in the late 1950s and early 1960s with Herbert Glance in 1957 and Charles Blair in 1960. They came up with a way to check every word someone typed against a list of right spellings, pointing out any that didn’t fit. These early systems couldn’t suggest fixes, but they were important first steps for spellchecking tools.

## 1965: Levenshtein distance algorithm

In 1965: Vladimir Levenshtein published the Levenshtein distance algorithm.

Let's say you wanted to turn the word "kitten" into "sitting". The goal is to do this in as few steps as possible.

This is where the Levenshtein Algorithm helps you figure out the minimum number of changes needed to transform one word into another. These changes can be:

Inserting a letter (e.g., adding an "s" to "kitten" to make "kittens").

Deleting a letter (e.g., removing the "k" from "kitten" to make "itten").

Replacing a letter (e.g., swapping the "k" in "kitten" with an "s" to make "sitten").


This first implementation matches the naive recursive way. This is later on improved by using dynamic programming.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6b0p5r0buq03qdipt12x.png)

## Early 1970s: Ralph Gorin created "Spell," a program

Early 1970s: Ralph Gorin created "Spell," a program that identified misspelled words and suggested plausible correct spellings with an edit distance of one, meaning corrections involving a single letter insertion, deletion, or substitution. In 1971, Ralph published his program making it publicly available and quickly spreading its use worldwide. A limitation of this program was its inability to calculate plausible words beyond an edit distance of one.

## 1974: Robert Wagner and Michael Fischer introduced dynamic programming

1974: Robert Wagner and Michael Fischer introduced dynamic programming to improve the efficiency of calculating edit distance. The Wagner-Fischer algorithm broke down complex problems into simpler subproblems, solving each subproblem once and storing the solutions to avoid repetitive work.

Here is a visualization in claude: https://claude.site/artifacts/1bb87561-f087-4ad8-9a95-df5d2a30262e

## 1980s and 1990s: Microsoft Word

1980s and 1990s: Programs like Word Check and Microsoft Word used more evolved and optimized versions of these algorithms

## 2000 and beyond Spell Checkers: More Than Just Simple Fixes

### Understanding the Sentence
Today’s spell checkers don’t just look at words by themselves. They use smart tricks (called Natural Language Processing, or NLP) to figure out what a whole sentence means. For example, a word might be spelled right on its own, but if it doesn’t make sense in the sentence, the spell checker can catch it. This makes them better at avoiding mistakes and helps them work smoother for us.

### Guessing What You Meant
A lot of spell checkers use an idea called the "noisy channel model." It’s like treating a misspelled word as a scrambled version of the right one. Then, it uses math and guesses to pick the word you probably wanted. A guy named Peter Norvig made a simple version of this popular by mixing how often words show up with how close they are to what you typed.

### Learning From Tons of Words
Now, spell checkers are getting even smarter with things like machine learning and deep learning. These are like teaching a computer brain (neural networks) to study huge piles of text. This helps them fix tricky stuff—like words that sound the same (like "their" and "there"), mistakes based on the sentence, and even grammar—not just basic typos.

### Fitting You Perfectly
Spell checkers today can also change to fit you. You can add your own special words (like job terms or names) to a custom list, and they’ll learn from the fixes you make over time. This way, they keep up with new words or weird spellings you use a lot.

I hope this brief introduction sparked your interest in spell checkers. Give it a try yourself!

Happy coding! :)