# [242. Valid Anagram (Easy)](https://leetcode.com/problems/valid-anagram/)

<p>Given two strings <code>s</code> and <code>t</code>, return <code>true</code> <em>if</em> <code>t</code> <em>is an anagram of</em> <code>s</code><em>, and</em> <code>false</code> <em>otherwise</em>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = "anagram", t = "nagaram"
<strong>Output:</strong> true
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = "rat", t = "car"
<strong>Output:</strong> false
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length, t.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code> and <code>t</code> consist of lowercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> What if the inputs contain Unicode characters? How would you adapt your solution to such a case?</p>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Spotify](https://leetcode.com/company/spotify), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Snapchat](https://leetcode.com/company/snapchat), [Oracle](https://leetcode.com/company/oracle), [Affirm](https://leetcode.com/company/affirm), [JPMorgan](https://leetcode.com/company/jpmorgan)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:

- [Group Anagrams (Medium)](https://leetcode.com/problems/group-anagrams/)
- [Palindrome Permutation (Easy)](https://leetcode.com/problems/palindrome-permutation/)
- [Find All Anagrams in a String (Medium)](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/valid-anagram/
# Author: Duy Tran
# Time: O(N)
# Space: O(1), O(26)
# Histogram every words
# +1 for each words in s
# -1 for each words in t
# check if thing is 0, which is balance count

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        d = dict()
        for c in s:
            d[c] = d.get(c, 0) + 1
        for c in t:
            if c not in d:
                return False
            d[c] = d.get(c, 0) - 1
        for c in d:
            if d[c] != 0:
                return False
        return True

```
