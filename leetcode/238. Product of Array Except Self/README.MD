# [238. Product of Array Except Self (Medium)](https://leetcode.com/problems/product-of-array-except-self/)

<p>Given an integer array <code>nums</code>, return <em>an array</em> <code>answer</code> <em>such that</em> <code>answer[i]</code> <em>is equal to the product of all the elements of</em> <code>nums</code> <em>except</em> <code>nums[i]</code>.</p>

<p>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</p>

<p>You must write an algorithm that runs in&nbsp;<code>O(n)</code>&nbsp;time and without using the division operation.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> [24,12,8,6]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [-1,1,0,-3,3]
<strong>Output:</strong> [0,0,9,0,0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-30 &lt;= nums[i] &lt;= 30</code></li>
	<li>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong>&nbsp;Can you solve the problem in <code>O(1)&nbsp;</code>extra&nbsp;space complexity? (The output array <strong>does not</strong> count as extra space for space complexity analysis.)</p>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Asana](https://leetcode.com/company/asana), [Apple](https://leetcode.com/company/apple), [Uber](https://leetcode.com/company/uber), [Adobe](https://leetcode.com/company/adobe), [American Express](https://leetcode.com/company/american-express), [Bloomberg](https://leetcode.com/company/bloomberg), [Oracle](https://leetcode.com/company/oracle), [Lyft](https://leetcode.com/company/lyft), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Groupon](https://leetcode.com/company/groupon), [Qualtrics](https://leetcode.com/company/qualtrics), [IBM](https://leetcode.com/company/ibm)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Prefix Sum](https://leetcode.com/tag/prefix-sum/)

**Similar Questions**:

- [Trapping Rain Water (Hard)](https://leetcode.com/problems/trapping-rain-water/)
- [Maximum Product Subarray (Medium)](https://leetcode.com/problems/maximum-product-subarray/)
- [Paint House II (Hard)](https://leetcode.com/problems/paint-house-ii/)
- [Minimum Difference in Sums After Removal of Elements (Hard)](https://leetcode.com/problems/minimum-difference-in-sums-after-removal-of-elements/)

## Solution 1.

prefix = product of `0` to `n`

postfix = product of `n` to `0`

```py
# OJ: https://leetcode.com/problems/product-of-array-except-self/
# Author: Duy Tran
# Time: O(N)
# Space: O(1) without counting result array

class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        res = [1 for _ in range(n)]
        prefix = 1
        for i in range(n):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(n-1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
        return res

```
