Problem 6: Contains Duplicate

Problem Statement

Given an integer array nums, return True if any value appears at least twice in the array, and return False if every element is distinct.


---

Example 1

nums = [1,2,3,1]

Output:
True

Explanation:

The number 1 appears twice.


---

Example 2

nums = [1,2,3,4]

Output:
False

Explanation:

All elements are unique.


---

Example 3

nums = [1,1,1,3,3,4,3,2,4,2]

Output:
True


---

Approach

Observation

The brute-force approach is to compare every element with every other element.

However, this requires O(n²) time.

A better approach is to use a Hash Set.

A Hash Set stores only unique elements.

While traversing the array:

If the current element is already in the set, a duplicate exists.

Otherwise, insert it into the set.



---

Intuition

Maintain a set called seen.

For every number:

If it already exists in seen, return True.

Otherwise, add it to the set.


If the loop completes without finding duplicates, return False.


---

Algorithm

Create an empty set

For each number in nums

    If number is already in the set

        Return True

    Otherwise

        Add the number to the set

Return False

'''
---

Python Code

def containsDuplicate(nums):

    seen = set()

    for num in nums:

        if num in seen:
            return True

        seen.add(num)

    return False


---

Dry Run

nums = [1,2,3,1]

seen = {}

----------------

num = 1

Not in seen

seen = {1}

----------------

num = 2

Not in seen

seen = {1,2}

----------------

num = 3

Not in seen

seen = {1,2,3}

----------------

num = 1

Already in seen

Return True


---

Why Use a Set?

A set provides constant-time average lookup.

Checking

num in seen

takes approximately O(1) time.

This makes the overall solution much faster than comparing every pair.


---

Time Complexity

We traverse the array exactly once.

Each lookup and insertion into the set takes O(1) on average.

Time Complexity: O(n)


---

Space Complexity

In the worst case, every element is unique.

The set stores all n elements.

Space Complexity: O(n)


---

Common Interview Mistakes

❌ Using a List Instead of a Set

seen = []

if num in seen:

List membership checking takes O(n) time.

Overall complexity becomes O(n²).


---

❌ Sorting the Array First

nums.sort()

Then checking adjacent elements works, but sorting itself takes O(n log n).

Although valid, it is not the most optimal solution.


---

❌ Forgetting That Sets Store Unique Values

A set automatically ignores duplicate insertions.

Example:

seen = {1,2,3}

seen.add(2)

seen

Output:

{1,2,3}

The duplicate is not stored.


---

Interview Takeaways

Whenever you need to quickly determine whether an element has been seen before, think of a Hash Set.

Sets are ideal for:

Duplicate detection

Membership checking

Unique element storage


This is one of the most common Hashing interview patterns.



---

Summary

Traverse the array once.

Store visited elements in a Hash Set.

If an element already exists in the set, return True.

If the traversal finishes without duplicates, return False.

Time Complexity: O(n)

Space Complexity: O(n)



---

Pattern Learned

This is your first Hashing problem.

The key pattern is:

> "Have I seen this element before?"



Whenever a problem asks about duplicates, uniqueness, or fast membership checking, a Hash Set is often the optimal choice. This pattern is widely used in problems such as Valid Anagram, Longest Consecutive Sequence, and many sliding window problems.