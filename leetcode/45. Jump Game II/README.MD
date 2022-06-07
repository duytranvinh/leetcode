# [45. Jump Game II (Medium)](https://leetcode.com/problems/jump-game-ii/)

<p>Given an array of non-negative integers <code>nums</code>, you are initially positioned at the first index of the array.</p>

<p>Each element in the array represents your maximum jump length at that position.</p>

<p>Your goal is to reach the last index in the minimum number of jumps.</p>

<p>You can assume that you can always reach the last index.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,3,1,1,4]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [2,3,0,1,4]
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 1000</code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [Microsoft](https://leetcode.com/company/microsoft), [Tesla](https://leetcode.com/company/tesla), [DoorDash](https://leetcode.com/company/doordash), [tiktok](https://leetcode.com/company/tiktok), [payu](https://leetcode.com/company/payu)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Greedy](https://leetcode.com/tag/greedy/)

**Similar Questions**:

- [Jump Game (Medium)](https://leetcode.com/problems/jump-game/)
- [Jump Game III (Medium)](https://leetcode.com/problems/jump-game-iii/)
- [Jump Game VII (Medium)](https://leetcode.com/problems/jump-game-vii/)

## Solution 1. Greedy

This problem is defined as Greedy but it's more like a BFS, sliding window problem

We start our window at `l = r = 0`

Then we find what's the `maxJump` we can jump in that window

Then we update `l = r + 1` and `r = maxJump`

We update our `res` step one by one at each sliding

```py
# OJ: https://leetcode.com/problems/jump-game-ii/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def jump(self, nums: List[int]) -> int:
        res = 0
        l = r = 0
        while r < len(nums) - 1:
            maxJump = 0
            for i in range(l, r + 1):
                maxJump  = max(maxJump, i + nums[i])
            l = r + 1
            r = maxJump
            res += 1
        return res

```
