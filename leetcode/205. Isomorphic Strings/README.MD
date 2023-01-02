# [205. Isomorphic Strings (Easy)](https://leetcode.com/problems/isomorphic-strings)

<p>Given two strings <code>s</code> and <code>t</code>, <em>determine if they are isomorphic</em>.</p>

<p>Two strings <code>s</code> and <code>t</code> are isomorphic if the characters in <code>s</code> can be replaced to get <code>t</code>.</p>

<p>All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> s = "egg", t = "add"
<strong>Output:</strong> true
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> s = "foo", t = "bar"
<strong>Output:</strong> false
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> s = "paper", t = "title"
<strong>Output:</strong> true
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>t.length == s.length</code></li>
	<li><code>s</code> and <code>t</code> consist of any valid ascii character.</li>
</ul>

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table), [String](https://leetcode.com/tag/string)

## Solution 1.

Map every character in each word to each other

![](https://leetcode.com/problems/isomorphic-strings/solutions/1261227/Figures/205/img2.png)

We need two map to do two-way conversion

![](https://leetcode.com/problems/isomorphic-strings/solutions/1261227/Figures/205/img3.png)

```py
# OJ: https://leetcode.com/problems/isomorphic-strings
# Author: Duy Tran
# Time: O(N)
# Space: O(1) - map of 26 characters

class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        d1, d2 = dict(), dict()
        for c1, c2 in zip(s, t):
            if (c1 in d1) and (d1[c1] != c2): return False
            if (c2 in d2) and (d2[c2] != c1): return False
            d1[c1] = c2
            d2[c2] = c1
        return True
```
