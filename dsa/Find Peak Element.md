# Problem 3: Find Peak Element

## Problem Statement

A **peak element** is an element that is **strictly greater than its adjacent elements**.

Given an integer array `nums`, return the index of **any one peak element**.

You may imagine that:

- `nums[-1] = -∞`
- `nums[n] = -∞`

This means the first and last elements each have one imaginary neighbor with value negative infinity.

You must solve the problem in **O(log n)** time complexity.

---

## Example 1

```
nums = [1,2,3,1]

Output:
2
```

Explanation:

```
        Peak
         ↓
1    2    3    1
```

Since **3 > 2** and **3 > 1**, index **2** is a peak.

---

## Example 2

```
nums = [1,2,1,3,5,6,4]

Output:
5
```

Explanation:

```
1    2    1    3    5    6    4
                    ↑
                  Peak
```

or

```
1    2    1    3    5    6    4
     ↑
   Peak
```

Both indices **1** and **5** are valid answers because both are peak elements.

---

# Key Observation

Unlike normal Binary Search, **we are not searching for a particular value**.

Instead, we are searching for a **position** that satisfies a condition:

```
nums[i] > nums[i-1]
AND
nums[i] > nums[i+1]
```

The trick is to observe the **slope** around the middle element.

---

# Intuition

At every middle element, compare it with its next element.

### Case 1

```
nums[mid] > nums[mid + 1]
```

Example

```
1  3  7  6  5
      ↑
```

We are on a **descending slope**.

A peak must exist on the **left side**, including `mid`.

So,

```
high = mid
```

---

### Case 2

```
nums[mid] < nums[mid + 1]
```

Example

```
1  3  5  7  8
      ↑
```

We are on an **ascending slope**.

A peak must exist on the **right side**.

So,

```
low = mid + 1
```

---

# Why Does This Work?

If we are climbing upward,

```
1 → 3 → 5 → 8
```

either:

- the array eventually goes down (forming a peak), or
- the last element becomes the peak because its right neighbor is `-∞`.

Similarly, if we are moving downward,

```
9 → 7 → 4 → 2
```

a peak must already exist on the left.

Therefore, we can safely discard half of the array in every iteration.

This satisfies the **O(log n)** requirement.

---

# Algorithm

```
low = 0
high = n - 1

while low < high

    mid = low + (high-low)//2

    if nums[mid] > nums[mid+1]
        high = mid

    else
        low = mid + 1

return low
```

---

# Python Code

```
def findPeakElement(nums):

    low = 0
    high = len(nums) - 1

    while low < high:

        mid = low + (high - low) // 2

        if nums[mid] > nums[mid + 1]:
            high = mid
        else:
            low = mid + 1

    return low
```

---

# Dry Run

```
nums = [1,2,3,1]

low = 0
high = 3

----------------

mid = 1

nums[mid] = 2
nums[mid+1] = 3

2 < 3

Move Right

low = 2

----------------

low = 2
high = 3

mid = 2

nums[mid] = 3
nums[mid+1] = 1

3 > 1

Move Left

high = 2

----------------

low = 2
high = 2

Loop Ends

Return 2
```

---

# Time Complexity

Each iteration discards half of the remaining search space.

**Time Complexity:** **O(log n)**

---

# Space Complexity

Only three variables are used.

- `low`
- `high`
- `mid`

**Space Complexity:** **O(1)**

---

# Common Interview Mistakes

### ❌ Using `while low <= high`

This problem should use:

```
while low < high
```

because we compare `nums[mid]` with `nums[mid + 1]`. Using `<=` can make `mid` equal to the last index, causing `mid + 1` to go out of bounds.

---

### ❌ Writing

```
high = mid - 1
```

Incorrect.

When:

```
nums[mid] > nums[mid+1]
```

`mid` itself **could be the peak**, so we must keep it in the search space.

Correct:

```
high = mid
```

---

### ❌ Returning `mid`

`mid` changes every iteration and is not guaranteed to be the final peak.

Return:

```
return low
```

At loop termination:

```
low == high
```

This index represents a valid peak element.

---

# Interview Takeaways

- This is **not** a standard Binary Search problem.
- We are searching for a **condition**, not a specific value.
- The decision is based on the **slope** (`nums[mid]` vs `nums[mid+1]`).
- Always remember:
    - Descending slope → search left (`high = mid`)
    - Ascending slope → search right (`low = mid + 1`)

---

# Summary

- A peak element is greater than its adjacent elements.
- Use Binary Search by analyzing the slope around `mid`.
- If `nums[mid] > nums[mid + 1]`, search the left half.
- Otherwise, search the right half.
- Continue until `low == high`.
- Return `low`, which is the index of a peak.
- **Time Complexity:** **O(log n)**
- **Space Complexity:** **O(1)**

---