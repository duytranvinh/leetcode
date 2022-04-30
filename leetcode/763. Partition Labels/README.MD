# [763. Partition Labels (Medium)](https://leetcode.com/problems/partition-labels/)

<p>You are given a string <code>s</code>. We want to partition the string into as many parts as possible so that each letter appears in at most one part.</p>

<p>Note that the partition is done so that after concatenating all the parts in order, the resultant string should be <code>s</code>.</p>

<p>Return <em>a list of integers representing the size of these parts</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "ababcbacadefegdehijhklij"
<strong>Output:</strong> [9,7,8]
<strong>Explanation:</strong>
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "eccbbbbdec"
<strong>Output:</strong> [10]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 500</code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/), [Greedy](https://leetcode.com/tag/greedy/)

**Similar Questions**:

- [Merge Intervals (Medium)](https://leetcode.com/problems/merge-intervals/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/partition-labels/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)
# Ref: https://www.youtube.com/watch?v=B7m8UmZE-vw

class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        #Find the the last index of each char
        last = {c: index for index, c in enumerate(s)}
        res = list()
        size = end = 0
        #update the end as the max of last[c]
        #when reach the end, conclude that answer
        #reset and continue
        for i, c in enumerate(s):
            size += 1
            end = max(end, last[c])
            if i == end:
                res.append(size)
                size = 0
        return res

```
