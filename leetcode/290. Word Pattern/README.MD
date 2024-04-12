# [290. Word Pattern (Easy)](https://leetcode.com/problems/word-pattern)

<p>Given a <code>pattern</code> and a string <code>s</code>, find if <code>s</code>&nbsp;follows the same pattern.</p>

<p>Here <b>follow</b> means a full match, such that there is a bijection between a letter in <code>pattern</code> and a <b>non-empty</b> word in <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> pattern = &quot;abba&quot;, s = &quot;dog cat cat dog&quot;
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> pattern = &quot;abba&quot;, s = &quot;dog cat cat fish&quot;
<strong>Output:</strong> false
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> pattern = &quot;aaaa&quot;, s = &quot;dog cat cat dog&quot;
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= pattern.length &lt;= 300</code></li>
	<li><code>pattern</code> contains only lower-case English letters.</li>
	<li><code>1 &lt;= s.length &lt;= 3000</code></li>
	<li><code>s</code> contains only lowercase English letters and spaces <code>&#39; &#39;</code>.</li>
	<li><code>s</code> <strong>does not contain</strong> any leading or trailing spaces.</li>
	<li>All the words in <code>s</code> are separated by a <strong>single space</strong>.</li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Zoho](https://leetcode.com/company/zoho), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Dropbox](https://leetcode.com/company/dropbox), [Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table), [String](https://leetcode.com/tag/string)

**Similar Questions**:

- [Isomorphic Strings (Easy)](https://leetcode.com/problems/isomorphic-strings)
- [Word Pattern II (Medium)](https://leetcode.com/problems/word-pattern-ii)

## Solution 1. Two hashmap

Use to hashmap to keep track of `charToWord` and `wordToChar`

There only 26 english char so maximum space is only `O(1)`

```py
# OJ: https://leetcode.com/problems/word-pattern
# Author: Duy Tran
# Time: O(N)
# Space: O(1)


class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        words = s.split(' ')
        if len(pattern) != len(words): return False
        charToWord = {}
        wordToChar = {}
        for c, w in zip(pattern, words):
          if c in charToWord and charToWord[c] != w: return False
          if w in wordToChar and wordToChar[w] != c: return False
          charToWord[c] = w
          wordToChar[w] = c
        return True

```
