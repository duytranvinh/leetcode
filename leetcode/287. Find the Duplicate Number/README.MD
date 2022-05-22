# [287. Find the Duplicate Number (Medium)](https://leetcode.com/problems/find-the-duplicate-number/)

<p>Given an array of integers <code>nums</code> containing&nbsp;<code>n + 1</code> integers where each integer is in the range <code>[1, n]</code> inclusive.</p>

<p>There is only <strong>one repeated number</strong> in <code>nums</code>, return <em>this&nbsp;repeated&nbsp;number</em>.</p>

<p>You must solve the problem <strong>without</strong> modifying the array <code>nums</code>&nbsp;and uses only constant extra space.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,3,4,2,2]
<strong>Output:</strong> 2
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [3,1,3,4,2]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>nums.length == n + 1</code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
	<li>All the integers in <code>nums</code> appear only <strong>once</strong> except for <strong>precisely one integer</strong> which appears <strong>two or more</strong> times.</li>
</ul>

<p>&nbsp;</p>
<p><b>Follow up:</b></p>

<ul>
	<li>How can we prove that at least one duplicate number must exist in <code>nums</code>?</li>
	<li>Can you solve the problem in linear runtime complexity?</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Uber](https://leetcode.com/company/uber), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Qualcomm](https://leetcode.com/company/qualcomm)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [Binary Search](https://leetcode.com/tag/binary-search/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/)

**Similar Questions**:

- [First Missing Positive (Hard)](https://leetcode.com/problems/first-missing-positive/)
- [Single Number (Easy)](https://leetcode.com/problems/single-number/)
- [Linked List Cycle II (Medium)](https://leetcode.com/problems/linked-list-cycle-ii/)
- [Missing Number (Easy)](https://leetcode.com/problems/missing-number/)
- [Set Mismatch (Easy)](https://leetcode.com/problems/set-mismatch/)

## Solution 1. Floyd's Cycle Detection

[Reference](https://www.youtube.com/watch?v=wjYnzkAhcNk)

**Phase 1**

With `fast` run 2 times faster than `slow`

`fast` and `slow` point will meet at some time if there is a cycle

**Phase 2**

As `slow` stuck in the cycle, we ask `slow2` come to help, to find the entrance of the cycle

<img src="https://www.codingninjas.com/blog/wp-content/uploads/2020/09/image-64.png" style="width: 500px; height: 242px;">

We have `slow` = x + y, and `fast` = (x + y + z) + y = x + 2y + z

2 `slow` = `fast`

2 (x + y) = x + 2y + z

=> 2x + 2y = x + 2y + z

=> x = z

```py
# OJ: https://leetcode.com/problems/find-the-duplicate-number/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
        #Phase 2
        slow2 = 0
        while True:
            slow = nums[slow]
            slow2 = nums[slow2]
            if slow == slow2:
                return slow

```
