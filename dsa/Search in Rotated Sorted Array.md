# Problem 4: Search in Rotated Sorted Array

## Problem Statement

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Before being passed to your function, the array is **rotated** at some pivot index.

For example,

```text
Original:

[0,1,2,4,5,6,7]

Rotated:

[4,5,6,7,0,1,2]
```

Given the rotated array `nums` and an integer `target`, return the index of the target if it exists; otherwise, return **-1**.

You must write an algorithm with **O(log n)** runtime complexity.

---

# Example 1

```python
nums = [4,5,6,7,0,1,2]
target = 0

Output:
4
```

---

# Example 2

```python
nums = [4,5,6,7,0,1,2]
target = 3

Output:
-1
```

---

# Key Observation

Although the entire array is not sorted,

**at least one half is always sorted.**

Example:

```text
4   5   6   7   0   1   2
            ↑
           mid
```

Left Half

```text
4 5 6 7
```

is sorted.

Right Half

```text
0 1 2
```

is also sorted.

At every iteration, one of the two halves is guaranteed to be sorted.

The idea is to:

1. Identify the sorted half.
    
2. Check whether the target lies inside that half.
    
3. If yes, search that half.
    
4. Otherwise, search the other half.
    

---

# Intuition

There are only two possibilities.

---

## Case 1 : Left Half is Sorted

Condition:

```python
nums[low] <= nums[mid]
```

Example

```text
4   5   6   7   0   1   2
L       M
```

Since

```text
4 <= 6
```

Left half is sorted.

Now check whether the target lies inside it.

```python
nums[low] <= target < nums[mid]
```

If true

```python
high = mid - 1
```

Otherwise

```python
low = mid + 1
```

---

## Case 2 : Right Half is Sorted

Otherwise,

```text
mid             high

7   0   1   2
```

Right half is sorted.

Now check

```python
nums[mid] < target <= nums[high]
```

If true

```python
low = mid + 1
```

Otherwise

```python
high = mid - 1
```

---

# Algorithm

```text
low = 0
high = n - 1

while low <= high

    mid = low + (high-low)//2

    if nums[mid] == target
        return mid

    if left half is sorted

        if target lies inside left half

            high = mid - 1

        else

            low = mid + 1

    else

        if target lies inside right half

            low = mid + 1

        else

            high = mid - 1

return -1
```

---

# Python Code

```python
def search(nums, target):

    low = 0
    high = len(nums) - 1

    while low <= high:

        mid = low + (high - low) // 2

        if nums[mid] == target:
            return mid

        # Left half is sorted
        if nums[low] <= nums[mid]:

            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1

        # Right half is sorted
        else:

            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1

    return -1
```

---

# Dry Run

```text
nums = [4,5,6,7,0,1,2]

target = 0

low = 0
high = 6

----------------

mid = 3

nums[mid] = 7

Left Half

4 5 6 7

is sorted

Target = 0

Not inside

Move Right

low = 4

----------------

low = 4
high = 6

mid = 5

nums[mid] = 1

Left Half

0 1

is sorted

Target lies inside

high = 4

----------------

low = 4
high = 4

mid = 4

nums[mid] = 0

Target Found

Return 4
```

---

# Time Complexity

In every iteration, one half of the search space is discarded.

**Time Complexity:** **O(log n)**

---

# Space Complexity

Only three variables are maintained.

- `low`
    
- `high`
    
- `mid`
    

**Space Complexity:** **O(1)**

---

# Common Interview Mistakes

### ❌ Forgetting to identify the sorted half

Many candidates immediately compare the target with `mid`, which is not enough.

The first step after checking `nums[mid] == target` should always be:

```python
if nums[low] <= nums[mid]:
```

This determines whether the **left half** is sorted.

---

### ❌ Using incorrect comparison operators

For the left half:

```python
nums[low] <= target < nums[mid]
```

For the right half:

```python
nums[mid] < target <= nums[high]
```

Mixing `<` and `<=` incorrectly can skip valid targets.

---

### ❌ Assuming both halves are unsorted

A rotated sorted array always has **at least one sorted half**.

This observation is the foundation of the solution.

---

# Interview Takeaways

- A rotated array is **not completely unsorted**.
    
- At every iteration:
    
    1. Find the sorted half.
        
    2. Check whether the target belongs to that half.
        
    3. Discard the other half.
        
- The search space is halved every iteration, preserving **O(log n)** complexity.
    

---

# Summary

- A rotated sorted array always contains one sorted half.
    
- Identify the sorted half using `nums[low] <= nums[mid]`.
    
- Determine whether the target lies within that half.
    
- Continue Binary Search on the appropriate half.
    
- Return the index if found; otherwise, return `-1`.
    
- **Time Complexity:** **O(log n)**
    
- **Space Complexity:** **O(1)**
    

---

### Pattern Learned

This problem introduces an important Binary Search pattern:

> **Even if an array appears unsorted, look for a hidden monotonic (sorted) property.**

Recognizing this hidden property allows Binary Search to be applied to problems that are not obviously sorted. This pattern is reused in problems such as **Find Minimum in Rotated Sorted Array** and other advanced Binary Search variants.