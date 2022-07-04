# [128. Longest Consecutive Sequence (Medium)](https://leetcode.com/problems/longest-consecutive-sequence/)

<p>Given an unsorted array of integers <code>nums</code>, return <em>the length of the longest consecutive elements sequence.</em></p>

<p>You must write an algorithm that runs in&nbsp;<code>O(n)</code>&nbsp;time.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [100,4,200,1,3,2]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The longest consecutive elements sequence is <code>[1, 2, 3, 4]</code>. Therefore its length is 4.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,3,7,2,5,8,4,6,0,1]
<strong>Output:</strong> 9
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Spotify](https://leetcode.com/company/spotify), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Facebook](https://leetcode.com/company/facebook), [Qualtrics](https://leetcode.com/company/qualtrics), [eBay](https://leetcode.com/company/ebay), [Morgan Stanley](https://leetcode.com/company/morgan-stanley)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Union Find](https://leetcode.com/tag/union-find/)

**Similar Questions**:

- [Binary Tree Longest Consecutive Sequence (Medium)](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/)
- [Find Three Consecutive Integers That Sum to a Given Number (Medium)](https://leetcode.com/problems/find-three-consecutive-integers-that-sum-to-a-given-number/)
- [Maximum Consecutive Floors Without Special Floors (Medium)](https://leetcode.com/problems/maximum-consecutive-floors-without-special-floors/)

## Solution 1.

The numbers are stored in a HashSet (or Set, in Python) to allow O(1) lookups, and we only attempt to build sequences from numbers that are NOT already part of a longer sequence.

This is accomplished by first ensuring that the `number - 1` in a sequence is not present, as that number would necessarily be part of a longer sequence.

Although the time complexity appears to be quadratic due to the `while` loop nested within the for loop, closer inspection reveals it to be linear.

Time Complexity:

Because the `while` loop is reached only when `currentNum` marks the beginning of a sequence (i.e. currentNum-1 is not present in nums)

The `while` loop can only run for `n` iterations throughout the entire runtime of the algorithm.

This means that despite looking like `O(n⋅n)` complexity, the nested loops actually run in `O(n)` time.

All other computations occur in constant time, so the overall runtime is linear.

```py
# OJ: https://leetcode.com/problems/longest-consecutive-sequence/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numSet = set(nums)
        longest = 0
        for n in nums:
            # check if it's the start of a sequence
            if (n-1) not in numSet:
                length = 1
                while (n + length) in numSet:
                    length += 1
                longest = max(length, longest)
        return longest

```
