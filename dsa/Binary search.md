# Problem 2: Binary Search

## Definition

Binary Search is an efficient searching algorithm used to find a target element in a **sorted** array.

Instead of checking every element one by one, Binary Search repeatedly divides the search space into two halves and determines which half may contain the target.

This reduces the number of comparisons significantly.

---

## Prerequisites

Binary Search can only be applied when:

- The array is **sorted** (Ascending or Descending).
- Random access to elements is available (Arrays).

---

## Key Idea

Instead of searching the entire array:

1. Find the middle element.
2. Compare it with the target.
3. If equal, return the index.
4. If the target is smaller, search the left half.
5. If the target is larger, search the right half.
6. Repeat until the element is found or the search space becomes empty.

---

## Algorithm

```
Start

low = 0
high = n - 1

While low <= high

    mid = low + (high - low) // 2

    if nums[mid] == target
        return mid

    else if nums[mid] < target
        low = mid + 1

    else
        high = mid - 1

Return -1
```

---

## Python Code

```
def binarySearch(nums, target):

    low = 0
    high = len(nums) - 1

    while low <= high:

        mid = low + (high - low) // 2

        if nums[mid] == target:
            return mid

        elif nums[mid] < target:
            low = mid + 1

        else:
            high = mid - 1

    return -1
```

---

# Why use

```
Linear Search

Checks every element.

Time Complexity

O(n)

-------------------------

Binary Search

Removes half of the search space every iteration.

Time Complexity

O(log n)
```

---

# Example

```
nums = [2,4,6,8,10,12,14]

target = 10

low = 0
high = 6

mid = 3

nums[mid] = 8

10 > 8

Discard left half

----------------------

low = 4
high = 6

mid = 5

nums[mid] = 12

10 < 12

Discard right half

----------------------

low = 4
high = 4

mid = 4

nums[mid] = 10

Found
```

---

# Time Complexity

Every iteration eliminates **half** of the remaining search space.

```
n

↓

n/2

↓

n/4

↓

n/8

↓

...

↓

1
```

Number of divisions:

**Time Complexity:** **O(log n)**

---

# Space Complexity

Iterative Binary Search uses only three variables:

- low
- high
- mid

**Space Complexity:** **O(1)**

---

# Common Interview Mistake

Instead of writing

```
mid = (low + high) // 2
```

Prefer

```
mid = low + (high - low) // 2
```

Reason:

In languages like Java, C++, and C, `low + high` may overflow when the array size is very large.

Although Python integers do not overflow in this way, using the second form is considered a best practice and is expected in interviews because it is language-independent.

---

# When to Think of Binary Search

Consider Binary Search when the problem involves:

- A sorted array
- Finding an element efficiently
- Searching for the first or last occurrence
- Rotated sorted arrays
- Monotonic conditions
- Finding the minimum or maximum satisfying a condition (**Binary Search on Answer**)

---

# Summary

- Binary Search works only on **sorted** data.
- Divide the search space into two halves in every iteration.
- Compare the middle element with the target.
- Discard one half based on the comparison.
- Repeat until the target is found or the search space becomes empty.
- **Time Complexity:** **O(log n)**
- **Space Complexity:** **O(1)**