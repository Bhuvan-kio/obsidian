Problem 9: Top K Frequent Elements

Problem Statement

Given an integer array nums and an integer k, return the k most frequent elements.

You may return the answer in any order.


---

Example 1

nums = [1,1,1,2,2,3]
k = 2

Output:
[1,2]

Explanation:

Frequency of each element:

1 → 3 times
2 → 2 times
3 → 1 time

The two most frequent elements are 1 and 2.


---

Example 2

nums = [1]
k = 1

Output:
[1]


---

Approach

Observation

First, count how many times each number appears.

For the above example:

1 → 3
2 → 2
3 → 1

Once we know the frequencies, we simply return the k numbers with the highest frequencies.

We use:

Dictionary → Count frequencies

Bucket Sort → Group numbers by their frequency



---

Intuition

Step 1: Count Frequencies

nums = [1,1,1,2,2,3]

Dictionary

{
1 : 3
2 : 2
3 : 1
}


---

Step 2: Create Frequency Buckets

The maximum possible frequency is len(nums).

Create buckets where:

Index = Frequency
Value = List of numbers

Frequency

0 → []

1 → [3]

2 → [2]

3 → [1]

4 → []

5 → []

6 → []


---

Step 3: Traverse Backwards

Start from the highest frequency.

Frequency 6

↓

5

↓

4

↓

3 → [1]

↓

2 → [2]

Collected 2 elements.

Answer:

[1,2]


---

Algorithm

Count frequencies using a dictionary

Create frequency buckets

Place each number into its frequency bucket

Traverse buckets from highest frequency to lowest

Collect numbers until k elements are obtained

Return the answer


---

Python Code

```
def topKFrequent(nums, k)
    count = {}
    for num in nums:
        count[num] = count.get(num, 0) + 1
    freq = [[] for _ in range(len(nums) + 1)]
    for num, c in count.items():
        freq[c].append(num)
    result = []
    for i in range(len(freq) - 1, 0, -1):
        for num in freq[i]:
            result.append(num)
            if len(result) == k:
                return result
```
---

Dry Run

nums = [1,1,1,2,2,3]

k = 2

------------------------

Dictionary

{
1 : 3
2 : 2
3 : 1
}

------------------------

Buckets

0 : []

1 : [3]

2 : [2]

3 : [1]

------------------------

Traverse Backwards

Frequency 3

Take 1

Answer = [1]

------------------------

Frequency 2

Take 2

Answer = [1,2]

Collected k elements

Return [1,2]


---

Time Complexity

Counting frequencies:

O(n)

Building buckets:

O(n)

Traversing buckets:

O(n)

Overall:

Time Complexity: O(n)


---

Space Complexity

Dictionary:

O(n)

Buckets:

O(n)

Overall:

Space Complexity: O(n)


---

Common Interview Mistakes

❌ Sorting the Dictionary

Many beginners do:

sorted(count.items(), key=lambda x: x[1], reverse=True)

Sorting takes:

O(n log n)

The interview specifically expects a solution better than sorting.


---

❌ Forgetting Bucket Size

The bucket size should be:

freq = [[] for _ in range(len(nums) + 1)]

The maximum frequency of an element can be equal to len(nums).


---

❌ Traversing Buckets from Start

Incorrect:

0 → 1 → 2 → ...

This gives the least frequent elements first.

Always traverse from the highest frequency.


---

Interview Takeaways

Use a Hash Map to count frequencies.

Bucket Sort is useful when the range of frequencies is known.

Instead of sorting by frequency, place elements directly into buckets.

This achieves O(n) time complexity.



---

Summary

Count the frequency of every number.

Create buckets where each index represents a frequency.

Place each number into its corresponding bucket.

Traverse buckets from highest frequency to lowest.

Stop after collecting k elements.

Time Complexity: O(n)

Space Complexity: O(n)



---

Pattern Learned

This problem introduces the Frequency Bucket pattern.

> When frequencies are limited to a known range (0 to n), Bucket Sort can replace sorting and achieve linear time.



This pattern is commonly used in:

Top K Frequent Words

Sort Characters by Frequency

Bucket Sort

Frequency-based ranking problems