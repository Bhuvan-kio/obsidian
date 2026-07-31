Problem 8: Group Anagrams

Problem Statement

Given an array of strings strs, group the anagrams together.

You can return the answer in any order.


---

Example 1

strs = ["eat","tea","tan","ate","nat","bat"]

Output:

[
    ["eat","tea","ate"],
    ["tan","nat"],
    ["bat"]
]


---

Example 2

strs = [""]

Output:

[
    [""]
]


---

Example 3

strs = ["a"]

Output:

[
    ["a"]
]


---

Approach

Observation

Two words are anagrams if they contain the same characters with the same frequencies.

Example:

eat
tea
ate

If we sort each word,

eat → aet
tea → aet
ate → aet

All of them produce the same sorted string.

That sorted string can be used as the key in a dictionary.


---

Intuition

Create a dictionary where:

Key = Sorted version of the word.

Value = List of words having that sorted form.


Example:

"aet" → ["eat","tea","ate"]

"ant" → ["tan","nat"]

"abt" → ["bat"]

Finally, return all the dictionary values.


---

Algorithm

Create an empty dictionary

For every word in strs

    Sort the word

    Use the sorted word as the key

    Append the original word to that key

Return all dictionary values


---

Python Code

```
from collections import defaultdict
def groupAnagrams(strs):
    groups = defaultdict(list)
    for word in strs:
        key = "".join(sorted(word))
        groups[key].append(word)
    return list(groups.values())
```


---

Dry Run

strs = ["eat","tea","tan","ate","nat","bat"]

--------------------------------

word = "eat"

sorted = "aet"

Dictionary

{
    "aet" : ["eat"]
}

--------------------------------

word = "tea"

sorted = "aet"

{
    "aet" : ["eat","tea"]
}

--------------------------------

word = "tan"

sorted = "ant"

{
    "aet" : ["eat","tea"],
    "ant" : ["tan"]
}

--------------------------------

word = "ate"

sorted = "aet"

{
    "aet" : ["eat","tea","ate"],
    "ant" : ["tan"]
}

--------------------------------

word = "nat"

sorted = "ant"

{
    "aet" : ["eat","tea","ate"],
    "ant" : ["tan","nat"]
}

--------------------------------

word = "bat"

sorted = "abt"

{
    "aet" : ["eat","tea","ate"],
    "ant" : ["tan","nat"],
    "abt" : ["bat"]
}

--------------------------------

Return

[
    ["eat","tea","ate"],
    ["tan","nat"],
    ["bat"]
]


---

Why Sort the Word?

Consider:

eat
tea
ate

All three words become:

aet

Since every anagram produces the same sorted string, it becomes a perfect dictionary key.


---

Time Complexity

Let:

n = Number of words

k = Maximum length of a word


Sorting each word takes O(k log k).

For n words:

Time Complexity: O(n × k log k)


---

Space Complexity

The dictionary stores every word once.

Space Complexity: O(n × k)


---

Common Interview Mistakes

❌ Using the Original Word as the Key

groups[word].append(word)

Different anagrams would go into different groups.


---

❌ Forgetting to Join After Sorting

key = sorted(word)

sorted() returns a list, which cannot be used as a dictionary key.

Correct:

key = "".join(sorted(word))


---

❌ Returning the Dictionary Instead of the Values

Incorrect:

return groups

Correct:

return list(groups.values())


---

Interview Takeaways

Group similar objects using a dictionary.

Create a canonical representation (sorted string) to identify equivalent items.

Sorting transforms every anagram into the same key.

defaultdict(list) makes grouping simpler by automatically creating empty lists.



---

Summary

Sort each word alphabetically.

Use the sorted word as the dictionary key.

Append the original word to the corresponding list.

Return all grouped lists.

Time Complexity: O(n × k log k)

Space Complexity: O(n × k)



---

Pattern Learned

This problem combines Hashing + String Manipulation.

> When multiple items should be grouped based on a common property, create a unique key that represents that property.



Here, the sorted word acts as the common key.

This grouping pattern is useful in problems involving:

Frequency grouping

Categorization

Bucketing similar data

Hash Map-based grouping