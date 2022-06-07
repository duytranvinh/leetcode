# [53. Maximum Subarray (Easy)](https://leetcode.com/problems/maximum-subarray/)

<p>Given an integer array <code>nums</code>, find the contiguous subarray (containing at least one number) which has the largest sum and return <em>its sum</em>.</p>

<p>A <strong>subarray</strong> is a <strong>contiguous</strong> part of an array.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [-2,1,-3,4,-1,2,1,-5,4]
<strong>Output:</strong> 6
<strong>Explanation:</strong> [4,-1,2,1] has the largest sum = 6.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [5,4,-1,7,8]
<strong>Output:</strong> 23
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> If you have figured out the <code>O(n)</code> solution, try coding another solution using the <strong>divide and conquer</strong> approach, which is more subtle.</p>

**Companies**:  
[LinkedIn](https://leetcode.com/company/linkedin), [Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Cisco](https://leetcode.com/company/cisco), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [JPMorgan](https://leetcode.com/company/jpmorgan), [Shopee](https://leetcode.com/company/shopee), [VMware](https://leetcode.com/company/vmware), [Oracle](https://leetcode.com/company/oracle), [ByteDance](https://leetcode.com/company/bytedance), [Docusign](https://leetcode.com/company/docusign), [Samsung](https://leetcode.com/company/samsung), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Salesforce](https://leetcode.com/company/salesforce), [ServiceNow](https://leetcode.com/company/servicenow)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:

- [Best Time to Buy and Sell Stock (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- [Maximum Product Subarray (Medium)](https://leetcode.com/problems/maximum-product-subarray/)
- [Degree of an Array (Easy)](https://leetcode.com/problems/degree-of-an-array/)
- [Longest Turbulent Subarray (Medium)](https://leetcode.com/problems/longest-turbulent-subarray/)
- [Maximum Absolute Sum of Any Subarray (Medium)](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray/)
- [Maximum Subarray Sum After One Operation (Medium)](https://leetcode.com/problems/maximum-subarray-sum-after-one-operation/)
- [Substring With Largest Variance (Hard)](https://leetcode.com/problems/substring-with-largest-variance/)

## Solution 1. Rolling Sum + Greedy

```py
# OJ: https://leetcode.com/problems/maximum-subarray/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        res = cur = nums[0]
        for n in nums[1:]:
            cur = max(n, cur + n)
            res = max(res, cur)
        return res

```
