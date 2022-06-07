# [55. Jump Game (Medium)](https://leetcode.com/problems/jump-game/)

<p>You are given an integer array <code>nums</code>. You are initially positioned at the array's <strong>first index</strong>, and each element in the array represents your maximum jump length at that position.</p>

<p>Return <code>true</code><em> if you can reach the last index, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,3,1,1,4]
<strong>Output:</strong> true
<strong>Explanation:</strong> Jump 1 step from index 0 to 1, then 3 steps to the last index.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [3,2,1,0,4]
<strong>Output:</strong> false
<strong>Explanation:</strong> You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Oracle](https://leetcode.com/company/oracle), [Google](https://leetcode.com/company/google), [Salesforce](https://leetcode.com/company/salesforce), [DoorDash](https://leetcode.com/company/doordash), [ByteDance](https://leetcode.com/company/bytedance), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [Flipkart](https://leetcode.com/company/flipkart), [Docusign](https://leetcode.com/company/docusign)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Greedy](https://leetcode.com/tag/greedy/)

**Similar Questions**:

- [Jump Game II (Medium)](https://leetcode.com/problems/jump-game-ii/)
- [Jump Game III (Medium)](https://leetcode.com/problems/jump-game-iii/)
- [Jump Game VII (Medium)](https://leetcode.com/problems/jump-game-vii/)

## Solution 1. Greedy

We walk from backward to the first index

If we can reach the first index, then it's `True`

Initially, we keep our `target` is last index

While looping backward, if `i + nums[i] >= target`, we update `target = i`

```py

# OJ: https://leetcode.com/problems/jump-game/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        target = n - 1
        for i in range(n - 1, -1, -1):
            if i + nums[i] >= target:
                target = i
        return True if target == 0 else False

```
