# [303. Range Sum Query - Immutable (Easy)](https://leetcode.com/problems/range-sum-query-immutable)

<p>Given an integer array <code>nums</code>, handle multiple queries of the following type:</p>

<ol>
	<li>Calculate the <strong>sum</strong> of the elements of <code>nums</code> between indices <code>left</code> and <code>right</code> <strong>inclusive</strong> where <code>left &lt;= right</code>.</li>
</ol>

<p>Implement the <code>NumArray</code> class:</p>

<ul>
	<li><code>NumArray(int[] nums)</code> Initializes the object with the integer array <code>nums</code>.</li>
	<li><code>int sumRange(int left, int right)</code> Returns the <strong>sum</strong> of the elements of <code>nums</code> between indices <code>left</code> and <code>right</code> <strong>inclusive</strong> (i.e. <code>nums[left] + nums[left + 1] + ... + nums[right]</code>).</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;NumArray&quot;, &quot;sumRange&quot;, &quot;sumRange&quot;, &quot;sumRange&quot;]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
<strong>Output</strong>
[null, 1, -1, -3]

<strong>Explanation</strong>
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= left &lt;= right &lt; nums.length</code></li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to <code>sumRange</code>.</li>
</ul>

**Companies**:
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Palantir Technologies](https://leetcode.com/company/palantir-technologies)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Design](https://leetcode.com/tag/design), [Prefix Sum](https://leetcode.com/tag/prefix-sum)

**Similar Questions**:

- [Range Sum Query 2D - Immutable (Medium)](https://leetcode.com/problems/range-sum-query-2d-immutable)
- [Range Sum Query - Mutable (Medium)](https://leetcode.com/problems/range-sum-query-mutable)
- [Maximum Size Subarray Sum Equals k (Medium)](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k)

## Solution 1. Brute Force

Save the init array and calculate the range sum

Then each query will be an O(n)

```py
# OJ: https://leetcode.com/problems/range-sum-query-immutable
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class NumArray:
    def __init__(self, nums: List[int]):
        self.arr = nums
    def sumRange(self, left: int, right: int) -> int:
      res = 0
      for i in range(left, right+1):
        res += self.arr[i]
      return res
# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)

```

## Solution 2. Prefix calculation

Pre-calculate the sum from begin to that index of the array

Then on query, just need to do right - left. Then it's O(1)

```py
# OJ: https://leetcode.com/problems/range-sum-query-immutable
# Author: Duy Tran
# Time: O()
# Space: O()

    def __init__(self, nums: List[int]):
        self.prefix = []
        cur = 0
        for n in nums:
          cur += n
          self.prefix.append(cur)
    def sumRange(self, left: int, right: int) -> int:
      r = self.prefix[right]
      l = self.prefix[left - 1] if left > 0 else 0
      return r - l
# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```
