# [1480. Running Sum of 1d Array (Easy)](https://leetcode.com/problems/running-sum-of-1d-array)

<p>Given an array <code>nums</code>. We define a running sum of an array as&nbsp;<code>runningSum[i] = sum(nums[0]&hellip;nums[i])</code>.</p>

<p>Return the running sum of <code>nums</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> [1,3,6,10]
<strong>Explanation:</strong> Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,1,1,1]
<strong>Output:</strong> [1,2,3,4,5]
<strong>Explanation:</strong> Running sum is obtained as follows: [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [3,1,2,10,1]
<strong>Output:</strong> [3,4,6,16,17]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 1000</code></li>
	<li><code>-10^6&nbsp;&lt;= nums[i] &lt;=&nbsp;10^6</code></li>
</ul>

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Prefix Sum](https://leetcode.com/tag/prefix-sum)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/running-sum-of-1d-array
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        if (len(nums) == 0):    return []
        sum = 0
        res = []
        for num in nums:
            sum += num
            res.append(sum)
        return res
```
