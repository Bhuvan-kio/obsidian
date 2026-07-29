Problem 7: Valid Anagram

Problem Statement

Given two strings s and t, return True if t is an anagram of s; otherwise, return False.

An anagram is a word or phrase formed by rearranging the letters of another word, using all the original characters exactly once.


---

Example 1

s = "anagram"
t = "nagaram"

Output:
True


---

Example 2

s = "rat"
t = "car"

Output:
False


---

Approach

Observation

Two strings are anagrams if:

They contain the same characters.

Every character appears the same number of times.


Instead of comparing characters one by one, we count the frequency of each character.

If both strings have identical frequencies, they are anagrams.


---

Intuition

We use a Hash Map (Dictionary) to count the occurrences of each character.

Steps:

1. If the lengths are different, return False.


2. Count the frequency of every character in s.


3. Count the frequency of every character in t.


4. Compare both dictionaries.


5. If they are equal, return True; otherwise, return False.




---

Algorithm

If lengths are different

    Return False

Create two empty dictionaries

Count characters in s

Count characters in t

Compare both dictionaries

If equal

    Return True

Else

    Return False


---

Python Code

def isAnagram(s, t):

    if len(s) != len(t):
        return False

    countS = {}
    countT = {}

    for char in s:
        countS[char] = countS.get(char, 0) + 1

    for char in t:
        countT[char] = countT.get(char, 0) + 1

    return countS == countT


---

Dry Run

s = "anagram"
t = "nagaram"

----------------

countS

a : 3
n : 1
g : 1
r : 1
m : 1

----------------

countT

n : 1
a : 3
g : 1
r : 1
m : 1

----------------

Both dictionaries are equal

Return True


---

Why Compare Frequencies?

Consider:

listen
silent

The order is different.

However,

l : 1
i : 1
s : 1
t : 1
e : 1
n : 1

Both words contain exactly the same characters with the same frequency.

Hence, they are anagrams.


---

Time Complexity

We traverse each string once.

Dictionary insertion and lookup take O(1) on average.

Time Complexity: O(n)


---

Space Complexity

The dictionaries store the frequency of each unique character.

In the worst case:

Space Complexity: O(n)

(For lowercase English letters only, this can be considered O(1) because there are at most 26 unique characters.)


---

Common Interview Mistakes

❌ Ignoring Length Check

if len(s) != len(t):
    return False

If the lengths differ, they cannot be anagrams.

Checking this first avoids unnecessary work.


---

❌ Comparing Sorted Strings

return sorted(s) == sorted(t)

This works but sorting takes O(n log n) time.

The Hash Map solution is more efficient with O(n) time.


---

❌ Counting Only One String

Some beginners count characters in only one string.

Both strings must have identical character frequencies.


---

Interview Takeaways

Think of a Hash Map whenever you need to count frequencies.

Frequency counting is a common pattern in:

Anagrams

Character counting

Word counting

Sliding Window problems




---

Summary

Two strings are anagrams if they contain the same characters with the same frequencies.

First check whether their lengths are equal.

Count character frequencies using two dictionaries.

Compare the dictionaries.

Time Complexity: O(n)

Space Complexity: O(n)



---

Pattern Learned

This problem introduces the Frequency Counting pattern.

> Whenever a problem asks "How many times does each element occur?" think of a Hash Map (Dictionary).



This pattern is reused in problems such as:

Group Anagrams

Top K Frequent Elements

Find All Anagrams in a String

Majority Element

Sliding Window frequency problems