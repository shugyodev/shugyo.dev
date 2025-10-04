---
layout: post
title:  "#0002 — The Things They Told You"
series: Coding Interview Fundamentals
date:   2025-10-04 23:33:00 +0200
categories: [interview]
---
This post continues from [{{ page.previous.title }}]({{ page.previous.url }}).
If you haven’t read that yet, do so, before continuing.

In this series, I will use Python, as it's the most popular language for coding interviews.
Some concepts are Python-specific, 
and there might not be a perfect equivalent of them in your preferred language, but it is what it is.
It's your responsibility to try to grasp the spirit of what I'm trying to convey, and apply it as appropriate.

**Problem Statement:**
```
Given two words, decide if they are anagrams. 
An anagram is a word or phrase formed by rearranging the letters of another,
such as THING and NIGHT. 
```

It doesn’t matter how difficult the task is, you're never completely in the dark. 
You can always start with the things you already know. Things the interviewers stated in the problem statement. The things they told you.

#### Tip#1 — Identify inputs and outputs

They may tweak the phrasing a bit, to make things less obvious, but usually it's fairly straightforward to tell
what are the inputs to the problem, and what is the expected output of the solution.

In our example, the inputs are `two words`, and the output tells if they are `anagrams or not`.
This is a function signature that (tries to) capture this information.

```python
def anagSol(w1, w2):
    pass
```

#### Tip#2 — Names are important (I hope you read my first post)

There are hardly any cases, when abbreviating a trivial name is really worth it. 
I'm not saying that you shouldn't try to make them as concise a possible, but don't compress further than what's necessary.
All modern IDE-s will autocomplete your variable names, so you don't need to worry about how much effort it is to type them out.

Additionally, `word1` and `word2` are more explicit than `w1` and `w2`.
In general you should try to avoid `0` and `1` in variable names, as they are too similar to `O` and `l`.
For this reason, I'd prefer `wordA` and `wordB` over `word1` and `word2`. 
If you don't want to indicate that they are words, you may even go with `a` and `b`.

Not only arguments need a good name. Functions too. Since it returns `True` or `False`, `is*`, `are*`, `has*`, etc. are good options.
To figure out what the function name should be, you just need to summarize what the function does. 
In our case, `areAnagrams` feels right. 
Trust me, readable and meaningful names are rare pleasure on interviews, 
and you would be surprised how well they can make you stand out.

```python
def areAnagrams(wordA, wordB):
    pass
```

#### Tip#3 — Conventions are important

Whatever your chosen language may be, spend some time getting familiar with its conventions. 
The [PEP8 style guide](https://peps.python.org/pep-0008/#function-and-variable-names) prefers `snake_case`, so go with that. 
Following conventions itself may not get you extra credits, but not following them may be perceived negatively. 
If you really want to squeeze out something positive here, you can articulate that you consciously use `snake_case`, because that is the Python convention.

```python
def are_anagrams(word_a, word_b):
    pass
```

#### Tip#4 — Types are important
    
Yes, Python allows you to omit [type annotation](https://docs.python.org/3/library/typing.html), and yes, you can grab a knife at the sharp end, but I don't recommend either.
There is a good [reason](https://www.artima.com/weblogs/viewpost.jsp?thread=85551) why it was introduced more than [ten years ago](https://peps.python.org/pep-0484/#rationale-and-goals).
Also, it makes a good impression, if you're aware of type hints, and use them.
I'd recommend doing it within the function signature, but not within the function body, there it may hurt readability.

```python
def are_anagrams(word_a: str, word_b: str) -> bool:
    pass
```

Well done! We formulated our basic knowledge about the problem into a function signature!
Reading until here might have taken you quite some time (especially if you read the links I'm providing), 
but in reality, you should get to a level, where this whole step happens in your head almost instantly, 
and it doesn't take much more time to note down the function signature then it takes to say 
_“So I’ll likely need a function that takes two strings, word_a and word_b, and returns a bool, that tells if they are anagrams. I’d call it are_anagrams.”_

This one little line may not seem much of an achievement to you, 
but you already hinted to the interviewers that you can extract some important information quickly, 
and you have a basic good taste for code design and style. All that within the first few seconds.

**⚡ Your Turn:** 
Try turning a few problem statements into function signatures, and summarise what you did in plain english.
I recommend going on [LeetCode](https://leetcode.com), and repeat: 
- Read the problem statements on the left (do not glance at the right)
- Come up with a clean function signature
- Come up with a concise summary of what you just did in plain English
- Read the signature provided by them on the right

This is a valuable exercise. Don't skip it!

Also, only because they provided a different signature from what you came up with, it doesn't mean theirs is better.

I know they use a `Solution` class, and expect the implementation within an instance method, which they usually name in `camelCase`. 

You don't need to do that.

When you’re ready (you find this step easy, even on hard problems), continue with [next post coming soon].
