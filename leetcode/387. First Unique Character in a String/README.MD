# [387. First Unique Character in a String (Easy)](https://leetcode.com/problems/first-unique-character-in-a-string/)

<p>Given a string <code>s</code>, <em>find the first non-repeating character in it and return its index</em>. If it does not exist, return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = "leetcode"
<strong>Output:</strong> 0
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = "loveleetcode"
<strong>Output:</strong> 2
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> s = "aabb"
<strong>Output:</strong> -1
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists of only lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Oracle](https://leetcode.com/company/oracle), [Facebook](https://leetcode.com/company/facebook), [Visa](https://leetcode.com/company/visa), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Yahoo](https://leetcode.com/company/yahoo), [Qualtrics](https://leetcode.com/company/qualtrics), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Queue](https://leetcode.com/tag/queue/), [Counting](https://leetcode.com/tag/counting/)

**Similar Questions**:

- [Sort Characters By Frequency (Medium)](https://leetcode.com/problems/sort-characters-by-frequency/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/first-unique-character-in-a-string/
# Author: Duy Tran
# Time: O(N)
# Space: O(1), O(26) for 26 english characters

class Solution:
    def firstUniqChar(self, s: str) -> int:
        d = dict()
        for c in s:
            d[c] = d.get(c, 0) + 1
        for index, c in enumerate(s):
            if d[c] == 1:
                return index
        return -1

```
