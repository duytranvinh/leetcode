# [1838. Frequency of the Most Frequent Element (Medium)](https://leetcode.com/problems/frequency-of-the-most-frequent-element/)

<p>The <strong>frequency</strong> of an element is the number of times it occurs in an array.</p>

<p>You are given an integer array <code>nums</code> and an integer <code>k</code>. In one operation, you can choose an index of <code>nums</code> and increment the element at that index by <code>1</code>.</p>

<p>Return <em>the <strong>maximum possible frequency</strong> of an element after performing <strong>at most</strong> </em><code>k</code><em> operations</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,4], k = 5
<strong>Output:</strong> 3<strong>
Explanation:</strong> Increment the first element three times and the second element two times to make nums = [4,4,4].
4 has a frequency of 3.</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,4,8,13], k = 5
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are multiple optimal solutions:
- Increment the first element three times to make nums = [4,4,8,13]. 4 has a frequency of 2.
- Increment the second element four times to make nums = [1,8,8,13]. 8 has a frequency of 2.
- Increment the third element five times to make nums = [1,4,13,13]. 13 has a frequency of 2.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [3,9,6], k = 2
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= k &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [PhonePe](https://leetcode.com/company/phonepe), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Binary Search](https://leetcode.com/tag/binary-search/), [Greedy](https://leetcode.com/tag/greedy/), [Sliding Window](https://leetcode.com/tag/sliding-window/), [Sorting](https://leetcode.com/tag/sorting/), [Prefix Sum](https://leetcode.com/tag/prefix-sum/)

**Similar Questions**:

- [Find All Lonely Numbers in the Array (Medium)](https://leetcode.com/problems/find-all-lonely-numbers-in-the-array/)

## Solution 1. Sliding Window

This is sliding window problem as long as we can sort the array.

The window is valid when `nums[i] * window.length <= sum + k`

Therefore, we shrink left when `nums[r] * (r - l + 1) > total + k`

Why this work?

Let look at at `[1, 2, 4]` at `k = 5`

We can make this into `[4, 4, 4]`

Notice the sum different between two, `1 + 2 + 4 = 7` and `4 + 4 + 4 = 12`

The different between two array is `5` which is our `k`

Therefore, if increment our array, the total will be `sum + k`

Then why `nums[r] * window.length`?

Because when all the number in the window are the same. It will be that `nums[r] = 4 * window.length = 4 * 3 = 12`

```py

# OJ: https://leetcode.com/problems/frequency-of-the-most-frequent-element/
# Author: Duy Tran
# Time: O(NlogN)
# Space: O(1)

class Solution:
    def maxFrequency(self, nums: List[int], k: int) -> int:
        nums.sort()
        l, r = 0, 0
        res, total = 0, 0
        while r < len(nums):
            total += nums[r]
            while nums[r] * (r - l + 1) > total + k:
                total -= nums[l]
                l += 1
            res = max(res, (r - l + 1))
            r += 1
        return res

```
