# [496. Next Greater Element I (Easy)](https://leetcode.com/problems/next-greater-element-i)

<p>The <strong>next greater element</strong> of some element <code>x</code> in an array is the <strong>first greater</strong> element that is <strong>to the right</strong> of <code>x</code> in the same array.</p>

<p>You are given two <strong>distinct 0-indexed</strong> integer arrays <code>nums1</code> and <code>nums2</code>, where <code>nums1</code> is a subset of <code>nums2</code>.</p>

<p>For each <code>0 &lt;= i &lt; nums1.length</code>, find the index <code>j</code> such that <code>nums1[i] == nums2[j]</code> and determine the <strong>next greater element</strong> of <code>nums2[j]</code> in <code>nums2</code>. If there is no next greater element, then the answer for this query is <code>-1</code>.</p>

<p>Return <em>an array </em><code>ans</code><em> of length </em><code>nums1.length</code><em> such that </em><code>ans[i]</code><em> is the <strong>next greater element</strong> as described above.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [4,1,2], nums2 = [1,3,4,2]
<strong>Output:</strong> [-1,3,-1]
<strong>Explanation:</strong> The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,<u>4</u>,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [<u>1</u>,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,<u>2</u>]. There is no next greater element, so the answer is -1.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [2,4], nums2 = [1,2,3,4]
<strong>Output:</strong> [3,-1]
<strong>Explanation:</strong> The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,<u>2</u>,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,<u>4</u>]. There is no next greater element, so the answer is -1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums1.length &lt;= nums2.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums1[i], nums2[i] &lt;= 10<sup>4</sup></code></li>
	<li>All integers in <code>nums1</code> and <code>nums2</code> are <strong>unique</strong>.</li>
	<li>All the integers of <code>nums1</code> also appear in <code>nums2</code>.</li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you find an <code>O(nums1.length + nums2.length)</code> solution?

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Uber](https://leetcode.com/company/uber), [Bloomberg](https://leetcode.com/company/bloomberg), [Microsoft](https://leetcode.com/company/microsoft), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [Facebook](https://leetcode.com/company/facebook), [Goldman Sachs](https://leetcode.com/company/goldman-sachs)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [Stack](https://leetcode.com/tag/stack), [Monotonic Stack](https://leetcode.com/tag/monotonic-stack)

**Similar Questions**:

- [Next Greater Element II (Medium)](https://leetcode.com/problems/next-greater-element-ii)
- [Next Greater Element III (Medium)](https://leetcode.com/problems/next-greater-element-iii)
- [Daily Temperatures (Medium)](https://leetcode.com/problems/daily-temperatures)
- [Sum of Subarray Ranges (Medium)](https://leetcode.com/problems/sum-of-subarray-ranges)
- [Sum of Total Strength of Wizards (Hard)](https://leetcode.com/problems/sum-of-total-strength-of-wizards)
- [Next Greater Element IV (Hard)](https://leetcode.com/problems/next-greater-element-iv)
- [Remove Nodes From Linked List (Medium)](https://leetcode.com/problems/remove-nodes-from-linked-list)
- [Smallest Missing Integer Greater Than Sequential Prefix Sum (Easy)](https://leetcode.com/problems/smallest-missing-integer-greater-than-sequential-prefix-sum)

## Solution 1. Brute Force

```py
# OJ: https://leetcode.com/problems/next-greater-element-i
# Author: Duy Tran
# Time: O(N * M)
# Space: O(N)


class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        h1 = { num:i for i, num in enumerate(nums1)}
        n, m = len(nums1), len(nums2)
        res = [-1] * n
        for i in range(m):
          if nums2[i] not in h1: continue
          for j in range(i + 1, m):
            if nums2[j] > nums2[i]:
              cur = h1[nums2[i]]
              res[cur] = nums2[j]
              break
        return res

```

## Solution 2. Stack

Since each number in the array is unique, we can use stack to solve this

We keep the stack in an decreasing order. Whenever we see a number that is bigger than the stack's top, we pop the stack and update the result with that big number

```py
# OJ: https://leetcode.com/problems/next-greater-element-i
# Author: Duy Tran
# Time: O(N + M)
# Space: O(N)

class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        h1 = { num:i for i, num in enumerate(nums1)}
        n, m = len(nums1), len(nums2)
        res = [-1] * n
        stack = []
        for i in range(m):
          cur = nums2[i]
          while stack and cur > stack[-1]:
            val = stack.pop()
            idx = h1[val]
            res[idx] = cur
          if cur in h1:
            stack.append(cur)
        return res
```
