# Problem 1: Two Sum (Brute Force)

### Problem Statement

Given an integer array `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input has exactly one solution, and you may not use the same element twice.

### Example

```
nums = [2, 7, 11, 15]
target = 9

Output:
[0, 1]
```

---

# Approach 1: Brute Force

### Idea

The simplest approach is to compare every element with every other element.

For each element:

- Select the current element.
- Check every element after it.
- If their sum equals the target, return their indices.

This approach guarantees finding the answer because every possible pair is examined.

---

# Python Code

```
def twoSum(nums, target):
    n = len(nums)

    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] + nums[j] == target:
                return [i, j]
```

---

# Dry Run

```
nums = [2,7,11,15]
target = 9

i = 0

    j = 1

    nums[0] + nums[1]
    2 + 7 = 9

Target found

Return [0,1]
```

---

# Time Complexity

Outer loop runs **n** times.

For each element, the inner loop may traverse almost the remaining array.

```
Worst Case

n + (n-1) + (n-2) + ...

≈ n²
```

**Time Complexity:** **O(n²)**

---

# Space Complexity

No extra data structures are used.

Only loop variables are required.

**Space Complexity:** **O(1)**

---

# Why is this not optimal?

The algorithm repeatedly checks many unnecessary pairs.

For example,

```
(2,7)

Later

(7,2) is never checked due to j=i+1,
but many other combinations are still explored.
```

As the array grows larger, checking every pair becomes inefficient.

---

# Key Observation

The problem does **not** ask for the values.

It asks for the **indices**.

While checking a number, instead of searching the rest of the array every time, we can ask:

> "Have I already seen the number that would complete the target?"

This observation leads to the **Hash Map** solution, reducing the time complexity from **O(n²)** to **O(n)**.

---

# Interview Takeaways

- This is the most straightforward solution.
- Easy to understand and implement.
- Useful as the first solution during interviews before discussing optimization.
- Demonstrates the brute-force thought process that interviewers often expect.

---

# Summary

- Compare every possible pair of elements.
- Return the indices when the sum equals the target.
- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)
- Forms the baseline for deriving the optimal Hash Map solution.