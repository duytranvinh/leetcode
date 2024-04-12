# [448. Find All Numbers Disappeared in an Array (Easy)](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array)

<p>Given an array <code>nums</code> of <code>n</code> integers where <code>nums[i]</code> is in the range <code>[1, n]</code>, return <em>an array of all the integers in the range</em> <code>[1, n]</code> <em>that do not appear in</em> <code>nums</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [4,3,2,7,8,2,3,1]
<strong>Output:</strong> [5,6]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1,1]
<strong>Output:</strong> [2]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you do it without extra space and in <code>O(n)</code> runtime? You may assume the returned list does not count as extra space.</p>

**Companies**:
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table)

**Similar Questions**:

- [First Missing Positive (Hard)](https://leetcode.com/problems/first-missing-positive)
- [Find All Duplicates in an Array (Medium)](https://leetcode.com/problems/find-all-duplicates-in-an-array)
- [Find Unique Binary String (Medium)](https://leetcode.com/problems/find-unique-binary-string)
- [Append K Integers With Minimal Sum (Medium)](https://leetcode.com/problems/append-k-integers-with-minimal-sum)
- [Replace Elements in an Array (Medium)](https://leetcode.com/problems/replace-elements-in-an-array)
- [Maximum Number of Integers to Choose From a Range I (Medium)](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-i)
- [Maximum Number of Integers to Choose From a Range II (Medium)](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-ii)

**Hints**:

- This is a really easy problem if you decide to use additional memory. For those trying to write an initial solution using additional memory, think <b>counters!</b>
- However, the trick really is to not use any additional space than what is already available to use. Sometimes, multiple passes over the input array help find the solution. However, there's an interesting piece of information in this problem that makes it easy to re-use the input array itself for the solution.
- The problem specifies that the numbers in the array will be in the range [1, n] where n is the number of elements in the array. Can we use this information and modify the array in-place somehow to find what we need?

## Solution 1. Set

```py
# OJ: https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        s = set(nums)
        n = len(nums)
        res = []
        for i in range(1, n+1):
          if i in s: continue
          res.append(i)
        return res

```

## Solution 2.

If they have the follow up question

Follow up: Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

They we can reuse the input array and mark it negative n already exist

```py
# OJ: https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        for n in nums:
          i = abs(n) - 1
          nums[i] = -1 * abs(nums[i])
        res = []
        for i, n in enumerate(nums):
          if n > 0:
            res.append(i+1)
        return res
```
