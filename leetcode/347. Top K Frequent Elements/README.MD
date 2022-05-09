# [347. Top K Frequent Elements (Medium)](https://leetcode.com/problems/top-k-frequent-elements/)

<p>Given an integer array <code>nums</code> and an integer <code>k</code>, return <em>the</em> <code>k</code> <em>most frequent elements</em>. You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,1,2,2,3], k = 2
<strong>Output:</strong> [1,2]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>k</code> is in the range <code>[1, the number of unique elements in the array]</code>.</li>
	<li>It is <strong>guaranteed</strong> that the answer is <strong>unique</strong>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Your algorithm's time complexity must be better than <code>O(n log n)</code>, where n is the array's size.</p>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Oracle](https://leetcode.com/company/oracle), [Uber](https://leetcode.com/company/uber), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Adobe](https://leetcode.com/company/adobe), [Cisco](https://leetcode.com/company/cisco), [Shopee](https://leetcode.com/company/shopee), [Twitter](https://leetcode.com/company/twitter), [Snapchat](https://leetcode.com/company/snapchat), [ByteDance](https://leetcode.com/company/bytedance), [Netflix](https://leetcode.com/company/netflix)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Bucket Sort](https://leetcode.com/tag/bucket-sort/), [Counting](https://leetcode.com/tag/counting/), [Quickselect](https://leetcode.com/tag/quickselect/)

**Similar Questions**:

- [Word Frequency (Medium)](https://leetcode.com/problems/word-frequency/)
- [Kth Largest Element in an Array (Medium)](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- [Sort Characters By Frequency (Medium)](https://leetcode.com/problems/sort-characters-by-frequency/)
- [Split Array into Consecutive Subsequences (Medium)](https://leetcode.com/problems/split-array-into-consecutive-subsequences/)
- [Top K Frequent Words (Medium)](https://leetcode.com/problems/top-k-frequent-words/)
- [K Closest Points to Origin (Medium)](https://leetcode.com/problems/k-closest-points-to-origin/)
- [Sort Features by Popularity (Medium)](https://leetcode.com/problems/sort-features-by-popularity/)

## Solution 1. Heap

```py
# OJ: https://leetcode.com/problems/top-k-frequent-elements/
# Author: Duy Tran
# Time: O(NlogN)
# Space: O(N)

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # if k == len(nums):
        #     return nums
        count = defaultdict(int)
        for num in nums:
            count[num] += 1
        return heapq.nlargest(k, count.keys(), key = lambda x: count[x])
```

## Solution 2. Bucket Sort

Bucket Sort requires know the size of the nums

We have: `k` is in the range `[1, the number of unique elements in the array]`, this mean worst case [1,1,1,1,1] so `k = len(nums)`

We find count of each number, using hashmap

Then, we build frequency array with `i` = count

Then, we take top k from frequency array

```py
# OJ: https://leetcode.com/problems/top-k-frequent-elements/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        n = len(nums)
        count = defaultdict(int)
        freq = [[] for _ in range(n + 1)]

        for num in nums:
            count[num] += 1

        # freq[i] = [nums]
        # i = count
        for num, cnt in count.items():
            freq[cnt].append(num)

        res = list()
        nFreq = len(freq)
        for i in range(nFreq - 1, 0, -1):
            for n in freq[i]:
                res.append(n)
                if len(res) == k: return res
        return res

```
