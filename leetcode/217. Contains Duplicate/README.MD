# [217. Contains Duplicate (Easy)](https://leetcode.com/problems/contains-duplicate/)

<p>Given an integer array <code>nums</code>, return <code>true</code> if any value appears <strong>at least twice</strong> in the array, and return <code>false</code> if every element is distinct.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> true
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> false
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,1,3,3,4,3,2,4,2]
<strong>Output:</strong> true
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [Yahoo](https://leetcode.com/company/yahoo), [tcs](https://leetcode.com/company/tcs), [Atlassian](https://leetcode.com/company/atlassian), [Intel](https://leetcode.com/company/intel)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:

- [Contains Duplicate II (Easy)](https://leetcode.com/problems/contains-duplicate-ii/)
- [Contains Duplicate III (Medium)](https://leetcode.com/problems/contains-duplicate-iii/)

## Solution 1. Hash Set

```py
# OJ: https://leetcode.com/problems/contains-duplicate/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        founded = set()
        for num in nums:
            if num in founded: return True
            founded.add(num)
        return False

```

## Solution 2. Sorting

Sort then find `if nums[i] == nums[i - 1]: return True`
