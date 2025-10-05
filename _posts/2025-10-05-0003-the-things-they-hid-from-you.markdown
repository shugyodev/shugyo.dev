---
layout: post
title:  "#0003 — The Things They Hid From You"
series: Coding Interview Fundamentals
date:   2025-10-05 00:33:00 +0200
categories: [interview]
---
This post continues from [{{ page.previous.title }}]({{ page.previous.url }}).
If you haven’t read that yet, do so, before continuing.

**Problem Statement:**
```
Given two words, decide if they are anagrams. 
An anagram is a word or phrase formed by rearranging the letters of another,
such as THING and NIGHT. 
```

**Previous State:**
```python
def are_anagrams(word_a: str, word_b: str) -> bool:
    pass
```

[Fail-fast systems](https://en.wikipedia.org/wiki/Fail-fast_system) indicate errors as early as possible. 
The earlier they are identified, the earlier they can be reacted on.
For efficient problem-solving, you need fail-fast thinking. 
While in the previous step (given enough practice) you didn't need to think much,
now, you have to start doing it.
Before jumping into an implementation, you should identify nuances and pitfalls, the things they hid from you.

#### Tip#1 — Identify the obvious base cases

This should be the easiest, as usually this is what the problem statement asks for,
and almost always the provided examples fall into this category.
Since we are working with a boolean function, we need to think of both positive and negative cases.

You can go very abstract, like:
```python
# "AB", "BA", True
# "AB", "BC", False
```

But I'd recommend using realistic, and sensible values, that help understanding:
```python
# "THING", "NIGHT", True
# "THING", "HELICOPTER", False
```

#### Tip#2 — Clarify details

Certain details are only present in the problem statement implicitly, or not at all. 
In interviews, this situation is often created intentionally, 
to test how well you can explore the problem.
However, in real life, it can and will happen naturally.
Often your clients believe they know what they want, and give that to you as requirements,
but often they might not even be aware of scenarios they didn't think of.
We don't know what we don't know.
This is why, as a developer it is not only your interest, but your duty, 
to help your client (and yourself) to get a good grasp of a problem.

An example of a missing detail would be handling letter case differences.
Should lowercase and uppercase form of the same letter be considered the same? Clarify it!

```python
# "Thing", "Night", True
```

An example of an implicit detail in our case would be concerning the inputs.
The problem statement clearly says, that two words will be the inputs,
however later it is stated that anagrams can be words or phrases.
Is it a mistake, or an intentional simplification? Clarify it!

```python
# "I AM LORD VOLDEMORT", "TOM MARVOLO RIDDLE", True
```

By the way, having the above clarified, you should update your mental (or written) representation of the function.
The arguments are not only words. This is a good excuse for me to go with `a` and `b`.

```python
def are_anagrams(a: str, b: str) -> bool:
    pass
```

From thinking about the above example, yet another implicit detail should pop up.
The number of spaces aren't the same. Anagrams are usually relate only to letters.
Even the problem statement says so. Should you ignore whitespaces, punctuation marks, etc.?

```python
# "I AM LORD VOLDEMORT!", "TOM.MARVOLO.RIDDLE", True
```

Lastly, I think it's quite clear, that rearrangement means you have to use all the letters,
so even if two words have the same letters, but not in the same number,
they are not anagrams, but better be safe than sorry. Clarify it!

```python
# "BOLD", "BLOOD", False
# "BATTER", "BARTER", False
```

I used AI, to come up with the last example. 
Even if I was a native english speaker, which I'm not, 
it may be difficult to come up with proper examples for every situation.
Don't waste too much time on this, as it might be seen as bad time management, at least on an interview.

In these cases, feel free to go abstract:

```python
# "AB", "ABB", False
# "AAB", "BAA", False
```

#### Tip#3 — Look for edge cases

Empty, missing, very small, very large inputs should also be thought of.
Since our inputs are strings, it is relatively straightforward to do.

```python
# "", "", True
# "AB"*10_000_000, "BA"*10_000_000, True
# "", None, error
# None, "", error
```

Should None be treated as error? Or should it be equivalent to something without letters?
Up to the client (interviewer) to decide.
What you need to show is that you thought about it, and you are flexible to implement what they ask for.

At this point, you have thought about a fair amount of scenarios. 
It is completely fine to finish, by asking the interviewer 
"This is all I could think of. Do you think this is sufficient, and we can start thinking about the solution, or is there anything I missed?"

Here is the full list so far:
```python
# "THING", "NIGHT", True               
# "THING", "HELICOPTER", False                     
# "Thing", "Night", True               
# "I AM LORD VOLDEMORT!", "TOM.MARVOLO.RIDDLE", True                                           
# "BOLD", "BLOOD", False               
# "BATTER", "BARTER", False                  
# "", "", True     
# "AB"*10_000_000, "BA"*10_000_000, True                               
# "", None, error        
# None, "", error        
```

If you selected good examples, just by looking at the inputs you should be able to tell what is the related scenario.
You might notice I have removed some cases, as they would be redundant.
I don't really need multiple examples of the same thing.
More importantly, I tried to come up with examples that close relate to one specific scenario.
This is why for example I only use lowercase letters in the single scenario, that is about upper/lower case differences.

You don't need to write down the scenario names, as it would take too much time on an interview, but I do it now once for you, for clarity.

```python
# basic positive case, anagrams             
# basic negative case, not anagrams
# ignore letter case differences
# ignore non-letters                                    
# ensure equal number of each letter (redundant, could also be removed)
# ensure equal number of each letter
# empty input
# large input
# missing right     
# missing left      
```

#### Tip#4 — Create a safety net

The power of disciplined practice is that it helps prevent issues getting out of control.
One very typical scenario is that the candidate jumps at the implementation without much thought,
writes something that almost works, and even tries the solution out for a few cases.
Then, when the interviewer throws a curve ball, that forces them to modify the implementation,
the modification while resolves the new scenario, but breaks an earlier one.
The candidate may or may not notice this, but the interviewer almost always does.

Since you already discussed the important scenarios with the interviewer, why not turn these comments into tests,
so you can later focus solely on the implementation? This idea is the basis of [regression testing](https://en.wikipedia.org/wiki/Regression_testing), 
and the scenarios we have defined are basically [unit test](https://en.wikipedia.org/wiki/Unit_testing) scenarios.

As an entry level candidate, are you expected to know this much, and go this far? Usually not.

Is it good if you can still do it (reasonably fast)? Definitely!

As a reminder, here is your signature:

```python
def are_anagrams(a: str, b: str) -> bool:
    pass
```

And your scenarios:

```python
# "THING", "NIGHT", True               
# "THING", "HELICOPTER", False                     
# "Thing", "Night", True               
# "I AM LORD VOLDEMORT!", "TOM.MARVOLO.RIDDLE", True                                           
# "BOLD", "BLOOD", False               
# "BATTER", "BARTER", False                  
# "", "", True     
# "AB"*10_000_000, "BA"*10_000_000, True                               
# "", None, error        
# None, "", error        
```

But how do you automate these?

The simplest approach would be to just call your function with the inputs, and print the result.

```python
print(are_anagrams("THING", "NIGHT")) # True               
```

This is fine, but after every run, you need to compare all the outputs to all the printed results.
Let the code do the comparison!

```python
print(are_anagrams("THING", "NIGHT") == True)               
```

This is definitely better. Now you just need to look at the output, and once they are all-True, you are good.
The problem is, that if a scenario in the middle fails, you need to count down which inputs that False belongs to.
Print the inputs that yielded the output! I'd recommend creating a little test function for this. 
Just copy-paste the original signature, add `test_` in front of it, and add the expected output as the last argument.
You can indicate it will not return anything, by adding `-> None` to the end.

```python
def test_are_anagrams(a: str, b: str, expected: bool) -> None:
    pass
```

If you formatted your 'notes' in comments in a `# "a", "b", expected_result` format, 
now you can harvest the fruits of your forethought, and easily turn them into invocations of this test helper function.

`print(test_are_anagrams("a", "b", expected_result))`

This test function should execute your logic, and compare the expected result with the actual result, and print an informative message.

```python
def test_are_anagrams(a: str, b: str, expected: bool) -> None:
    actual = are_anagrams(a, b)
    print(f'a: "{a}", b: "{b}"')
    print(f'    {expected == actual}')
```

This is much better now. Of course, the huge input will make this unreadable, but there are many ways to work around that.
- Reorganize the order of things printed, so length is not bothering (I will do this soon)
- You can decide to print only the first few characters of the input
- You can decide to temporarily comment out the input printing, whenever convenient
- You can decide to temporarily comment out large input case, whenever convenient

A significant improvement, for this example, it is sufficient. 
However, when the output is not a bool (so it's obvious why a test fails), it may make sense to print the expected vs actual values as well.

```python
def test_are_anagrams(a: str, b: str, expected: bool) -> None:
    actual = are_anagrams(a, b)
    print(f'a: "{a}", b: "{b}", expected: {expected}, actual: {actual}')
    print(f'    {expected == actual}')
```

Inspired by real unit tests, with a little effort you can turn the printed True (passing test) and False (failing test) 
into `"PASS"` and `"FAIL"` messages.

```python
def test_are_anagrams(a: str, b: str, expected: bool) -> None:
    actual = are_anagrams(a, b)
    print(f'a: "{a}", b: "{b}", expected: {expected}, actual: {actual}')
    print(f'    {"PASS" if expected == actual else "FAIL"}')
```

Finally, for readability, I would:
- have only one line printed per test case
- put PASS/FAIL on the front, so they vertically align, and easy to assess at a glance
- put the expected vs actual after pass or fail, as those values are short
- put the input values at the end, so their length doesn't impact readability

```python
def test_are_anagrams(a: str, b: str, expected: bool) -> None:
    actual = are_anagrams(a, b)
    print('{} - expected: {}, actual: {}, a: "{}", b: "{}"'.format(
        "PASS" if expected == actual else "FAIL",
        expected, actual, a, b
    ))
```

Similarly, you can create a helper for the error scenarios, if there are any.
In this case, you don't necessarily need an expected value input, unless you want to assert the error type, 
which in most interview situations is an overkill.

```python
def test_error_are_anagrams(a: str, b: str) -> None:
    try:
        actual = are_anagrams(a, b) 
    except:
           actual = "expected failure"
           result = "PASS" 
    else:
           result = "FAIL" 
    finally:
        print(f'{result} - actual: {actual}, a: "{a}", b: "{b}"')
```

Well done! We refined our understanding of the problem and weaved a safety net from it!

I shared as many intermediary steps as I could, to show the thought process, however in real life you will not have this much time.
This step is risky. If you cannot get to the final state above in a reasonable pace, 
some interviewers may (more or less rightfully) feel you are wasting time, especially if the problem is trivial.

One time management trick is when as you are asking the clarification questions and only capturing the answers in comments, 
it doesn't really feel like you are spending 'coding time'. You are just taking notes.
You ask questions, because the client (interviewer) did not specify the problem precisely enough, so you had to, 
and because the earlier they are clarified, the less rework is needed.

Only when there is an agreement on the requirements, start to write actual code.
- You can delay writing the signature to this point, but that doesn't really matter, as it has no functionality
- You should write the two test helpers at the very end, and very quickly, they can be memorized as a pattern
- You should turn the comments into test function invocations very quickly

Hopefully, your interviewers will appreciate that some time was spent on this, as they gained very valuable insight about you.
They now see that you look for clarity in requirements, you think fail-fast, and you think ahead, by creating automated tests.
If you can do the latter quickly (which you have to be able to, before moving on), they will know that this is not the 
first time you do it. They know that this speed can only be achieved by practice.

If you have fears that they might consider it a waste of time, be open about what you are going to do, 
and ask them if they are okay with it.
"Now that I have the requirements clear, do you mind if I spend a minute turning them into some basic automated tests?
So I don't have to test everything manually."

Also, **maybe it is a better time to write the test helpers later, at the end of the next step**.
Try both approaches and see what feels more natural to you.

**⚡ Your Turn:**
Use the function signatures from the previous exercise (you should have 10-15 at least), and
- articulate your understanding in the form of comments
- when in doubt what should be the output in a scenario, pick the most difficult (usually an error scenario, you need to practice this)
- create test helper functions
- turn the comments into test helper function invocations

This is a crucial exercise. Don't skip it!

When you’re ready (you find this step difficult, even on easy problems), continue with [next post coming soon].

