# [268. Missing Number (Easy)](https://leetcode.com/problems/missing-number/)

<p>Given an array <code>nums</code> containing <code>n</code> distinct numbers in the range <code>[0, n]</code>, return <em>the only number in the range that is missing from the array.</em></p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [3,0,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [9,6,4,2,3,5,7,0,1]
<strong>Output:</strong> 8
<strong>Explanation:</strong> n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= n</code></li>
	<li>All the numbers of <code>nums</code> are <strong>unique</strong>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you implement a solution using only <code>O(1)</code> extra space complexity and <code>O(n)</code> runtime complexity?</p>

**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Salesforce](https://leetcode.com/company/salesforce), [VMware](https://leetcode.com/company/vmware), [Nvidia](https://leetcode.com/company/nvidia)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Math](https://leetcode.com/tag/math/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:

- [First Missing Positive (Hard)](https://leetcode.com/problems/first-missing-positive/)
- [Single Number (Easy)](https://leetcode.com/problems/single-number/)
- [Find the Duplicate Number (Medium)](https://leetcode.com/problems/find-the-duplicate-number/)
- [Couples Holding Hands (Hard)](https://leetcode.com/problems/couples-holding-hands/)
- [Find Unique Binary String (Medium)](https://leetcode.com/problems/find-unique-binary-string/)

## Solution 1. Bit Manipulation - XOR

```py
# OJ: https://leetcode.com/problems/missing-number/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
# [0,n]
# we have a^a (same number) = 0
# if we ^ all number
# the missing num will show up at the end
    def missingNumber(self, nums: List[int]) -> int:
        n = len(nums)
        res = len(nums)
        for i in range (n):
            res ^= i ^ nums[i]
        return res
```

## Solution 2. Gauss' Formula

```py
# OJ: https://leetcode.com/problems/missing-number/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        n = len(nums)
        # Gauss' Formula
        # sum of [0,n] = (n * (n+1)) / 2
        expected = n * (n+1) // 2
        actual = sum(nums)
        return expected - actual
```
