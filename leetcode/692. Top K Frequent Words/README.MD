# [692. Top K Frequent Words (Medium)](https://leetcode.com/problems/top-k-frequent-words/)

<p>Given an array of strings <code>words</code> and an integer <code>k</code>, return <em>the </em><code>k</code><em> most frequent strings</em>.</p>

<p>Return the answer <strong>sorted</strong> by <strong>the frequency</strong> from highest to lowest. Sort the words with the same frequency by their <strong>lexicographical order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["i","love","leetcode","i","love","coding"], k = 2
<strong>Output:</strong> ["i","love"]
<strong>Explanation:</strong> "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
<strong>Output:</strong> ["the","is","sunny","day"]
<strong>Explanation:</strong> "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 500</code></li>
	<li><code>1 &lt;= words[i] &lt;= 10</code></li>
	<li><code>words[i]</code> consists of lowercase English letters.</li>
	<li><code>k</code> is in the range <code>[1, The number of <strong>unique</strong> words[i]]</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong> Could you solve it in <code>O(n log(k))</code> time and <code>O(n)</code> extra space?</p>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [Facebook](https://leetcode.com/company/facebook), [Yahoo](https://leetcode.com/company/yahoo), [Apple](https://leetcode.com/company/apple), [Two Sigma](https://leetcode.com/company/two-sigma), [Goldman Sachs](https://leetcode.com/company/goldman-sachs)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Trie](https://leetcode.com/tag/trie/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Bucket Sort](https://leetcode.com/tag/bucket-sort/), [Counting](https://leetcode.com/tag/counting/)

**Similar Questions**:

- [Top K Frequent Elements (Medium)](https://leetcode.com/problems/top-k-frequent-elements/)
- [K Closest Points to Origin (Medium)](https://leetcode.com/problems/k-closest-points-to-origin/)
- [Sort Features by Popularity (Medium)](https://leetcode.com/problems/sort-features-by-popularity/)

## Solution 1. Bucket Sort

Similar to [347. Top K Frequent Elements](/leetcode/347.%20Top%20K%20Frequent%20Elements/)

```py
# OJ: https://leetcode.com/problems/top-k-frequent-words/
# Author: Duy Tran
# Time: O(NlogN)
# Space: O(N)

class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        words.sort()
        n = len(words)
        count = defaultdict(int)
        freq = [[] for _ in range(n + 1)]

        for w in words:
            count[w] += 1
        for w, cnt in count.items():
            freq[cnt].append(w)

        res = list()
        nFreq = len(freq)
        for i in range(n - 1, 0, -1):
            for w in freq[i]:
                res.append(w)
                if len(res) == k:
                    return res
        return res
```
