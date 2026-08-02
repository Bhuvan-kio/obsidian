Problem 10: Product of Array Except Self

Problem Statement

Given an integer array nums, return an array answer such that:

answer[i] = Product of all elements in nums except nums[i]

You must not use division and should solve it in O(n) time.


---

Example 1

nums = [1,2,3,4]

Output:
[24,12,8,6]

Explanation:

Index 0

2 × 3 × 4 = 24

----------------

Index 1

1 × 3 × 4 = 12

----------------

Index 2

1 × 2 × 4 = 8

----------------

Index 3

1 × 2 × 3 = 6


---

Example 2

nums = [-1,1,0,-3,3]

Output:
[0,0,9,0,0]


---

Approach

Observation

Using two nested loops would calculate every product separately.

Time Complexity = O(n²)

We need an O(n) solution.

The key idea is:

For every index,

Product Except Self

=

(Product of all elements on the Left)

×

(Product of all elements on the Right)

Instead of multiplying every element repeatedly, we precompute:

Prefix Products (Left)

Suffix Products (Right)



---

Intuition

For

nums = [1,2,3,4]

Prefix Product

Each position stores the product of all elements before it.

Index

0   1   2   3

Nums

1   2   3   4

----------------

Prefix

1   1   2   6

Explanation:

Prefix[0] = 1

(No elements on the left)

----------------

Prefix[1]

1

----------------

Prefix[2]

1 × 2 = 2

----------------

Prefix[3]

1 × 2 × 3 = 6


---

Suffix Product

Each position stores the product of all elements after it.

Nums

1   2   3   4

----------------

Suffix

24  12  4  1

Explanation:

Suffix[3] = 1

(No elements on the right)

----------------

Suffix[2]

4

----------------

Suffix[1]

3 × 4 = 12

----------------

Suffix[0]

2 × 3 × 4 = 24


---

Final Answer

Multiply Prefix × Suffix.

Prefix

1   1   2   6

Suffix

24  12  4   1

----------------

Answer

24  12  8   6


---

Optimized Approach (O(1) Extra Space)

Instead of storing separate Prefix and Suffix arrays, we use the answer array itself.

Step 1

Store Prefix Products inside answer.

answer

1   1   2   6

Step 2

Traverse from right to left while maintaining a running suffix product.

suffix = 1

answer[3] = 6 × 1 = 6

suffix = 4

----------------

answer[2] = 2 × 4 = 8

suffix = 12

----------------

answer[1] = 1 × 12 = 12

suffix = 24

----------------

answer[0] = 1 × 24 = 24

Final answer:

24 12 8 6


---

Algorithm

Create answer array

Store Prefix Products

Initialize suffix = 1

Traverse from right to left

Multiply answer[i] by suffix

Update suffix

Return answer


---

Python Code

```
def productExceptSelf(nums):
    n = len(nums)
    answer = [1] * n
    prefix = 1
    for i in range(n):
        answer[i] = prefix
        prefix *= nums[i]
    suffix = 1
    for i in range(n - 1, -1, -1):
        answer[i] *= suffix
        suffix *= nums[i]
    return answer

```

---

Dry Run

nums = [1,2,3,4]

----------------

Prefix Pass

answer

1 1 2 6

----------------

suffix = 1

i = 3

answer

1 1 2 6

suffix = 4

----------------

i = 2

answer

1 1 8 6

suffix = 12

----------------

i = 1

answer

1 12 8 6

suffix = 24

----------------

i = 0

answer

24 12 8 6

Return answer


---

Time Complexity

We traverse the array twice.

O(n) + O(n)

Time Complexity: O(n)


---

Space Complexity

Ignoring the output array (which doesn't count as extra space in this problem):

Prefix variable

Suffix variable


Extra Space Complexity: O(1)


---

Common Interview Mistakes

❌ Using Division

total_product = product(nums)

answer[i] = total_product // nums[i]

The problem explicitly forbids using division.


---

❌ Using Nested Loops

for i in range(n):
    for j in range(n):

This results in O(n²) time, which is too slow.


---

❌ Confusing Prefix and Suffix

Remember:

Prefix → Product of elements before the current index.

Suffix → Product of elements after the current index.


The current element is never included.


---

Interview Takeaways

Prefix and Suffix products are powerful techniques for range-based computations.

Reusing the output array helps achieve O(1) extra space.

This is one of the most frequently asked array interview problems.



---

Summary

Compute the product of all elements to the left of each index.

Compute the product of all elements to the right while traversing backwards.

Multiply both values to obtain the final answer.

Avoid division.

Time Complexity: O(n)

Extra Space Complexity: O(1)



---

Pattern Learned

This problem introduces the Prefix–Suffix Pattern.

> When the answer for each index depends on all elements before and after it, think of Prefix and Suffix computations.



This pattern is widely used in:

Trapping Rain Water

Maximum Product Subarray

Range Product and Prefix Sum problems

Dynamic programming on arrays