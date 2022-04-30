# [345. Reverse Vowels of a String (Easy)](https://leetcode.com/problems/reverse-vowels-of-a-string/)

<p>Given a string <code>s</code>, reverse only all the vowels in the string and return it.</p>

<p>The vowels are <code>'a'</code>, <code>'e'</code>, <code>'i'</code>, <code>'o'</code>, and <code>'u'</code>, and they can appear in both cases.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> s = "hello"
<strong>Output:</strong> "holle"
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> s = "leetcode"
<strong>Output:</strong> "leotcede"
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 3 * 10<sup>5</sup></code></li>
	<li><code>s</code> consist of <strong>printable ASCII</strong> characters.</li>
</ul>

**Companies**:  
[Bloomberg](https://leetcode.com/company/bloomberg)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:

- [Reverse String (Easy)](https://leetcode.com/problems/reverse-string/)
- [Remove Vowels from a String (Easy)](https://leetcode.com/problems/remove-vowels-from-a-string/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/reverse-vowels-of-a-string/
# Author: Duy Tran
# Time: O(N)
# Space: O(L) for the length of S

class Solution:
    def isVowel(self, s, index):
        c = s[index].lower()
        return c == 'a' or c == 'e' or c == 'i' or c =='o' or c == 'u'
    def swapChar(self, s, lo, hi):
        tmp = s[lo]
        s[lo] = s[hi]
        s[hi] = tmp
    def reverseVowels(self, s: str) -> str:
        lo = 0
        hi = len(s) - 1
        res = list(s)
        while(lo < hi):
            loVowel = self.isVowel(res, lo)
            hiVowel = self.isVowel(res, hi)
            if loVowel and hiVowel:
                self.swapChar(res, lo, hi)
                lo += 1
                hi -= 1
            if not loVowel:
                lo += 1
            if not hiVowel:
                hi -= 1
        return "".join(res)
```
