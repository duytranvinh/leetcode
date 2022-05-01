# [28. Implement strStr() (Easy)](https://leetcode.com/problems/implement-strstr/)

<p>Implement <a href="http://www.cplusplus.com/reference/cstring/strstr/" target="_blank">strStr()</a>.</p>

<p>Given two strings <code>needle</code> and <code>haystack</code>, return the index of the first occurrence of <code>needle</code> in <code>haystack</code>, or <code>-1</code> if <code>needle</code> is not part of <code>haystack</code>.</p>

<p><strong>Clarification:</strong></p>

<p>What should we return when <code>needle</code> is an empty string? This is a great question to ask during an interview.</p>

<p>For the purpose of this problem, we will return 0 when <code>needle</code> is an empty string. This is consistent to C's <a href="http://www.cplusplus.com/reference/cstring/strstr/" target="_blank">strstr()</a> and Java's <a href="https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)" target="_blank">indexOf()</a>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> haystack = "hello", needle = "ll"
<strong>Output:</strong> 2
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> haystack = "aaaaa", needle = "bba"
<strong>Output:</strong> -1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= haystack.length, needle.length &lt;= 10<sup>4</sup></code></li>
	<li><code>haystack</code> and <code>needle</code> consist of only lowercase English characters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/), [String Matching](https://leetcode.com/tag/string-matching/)

**Similar Questions**:

- [Shortest Palindrome (Hard)](https://leetcode.com/problems/shortest-palindrome/)
- [Repeated Substring Pattern (Easy)](https://leetcode.com/problems/repeated-substring-pattern/)

## Solution 1. Knuth-Morris-Pratt (KMP) for pattern searching

```py
# OJ: https://leetcode.com/problems/implement-strstr/
# Author: Duy Tran
# Time: O(N + M), N is length of haystack, M is length of needle
# Space: O(M)

class Solution:
    # Longest proper prefix
    def lps(self, s):
        lps = [0 for _ in s]
        prev = 0
        i = 1
        while i < len(s):
            # if the pattern is matching
            if s[i] == s[prev]:
                lps[i] = prev + 1
                i += 1
                prev += 1
            # if it is not matching, then move on
            elif prev == 0:
                lps[i] = 0
                i += 1
            # keep backtrack the pattern
            else:
                prev = lps[prev - 1]
        return lps

    #Knuth-Morris-Pratt
    def kmp(self, s, t):
        if t == "": return 0
        lps = self.lps(t)
        n = len(s)
        m = len(t)
        i = j = 0
        while i < n:
            # if the pattern is matching
            if s[i] == t[j]:
                i += 1
                j += 1
            else:
                # if it is not matching, and no previous pattern
                # move on
                if j == 0:
                    i += 1
                # if it is not matching, keep backtrack the previous pattern
                else:
                    j = lps[j - 1]
            if j == m:
                return i - m
        return -1


    def strStr(self, haystack: str, needle: str) -> int:
        return self.kmp(haystack, needle)

```

## Solution 2. KMP, but more advanced

```py
# OJ: https://leetcode.com/problems/implement-strstr/
# Author: Duy Tran
# Time: O(N + M)
# Space: O(M)

class Solution:
    def strStr(self, haystack: str, needle: str) -> int:

        def getLPS(s):
            m, prev = len(s), 0
            lps = [0 for _ in s]
            for i in range(1, m):
                while s[i] != s[prev] and prev > 0:
                    prev = lps[prev - 1]
                if s[i] == s[prev]:
                    prev += 1
                    lps[i] = prev
            return lps

        def kmp(s, p):
            lps = getLPS(p)
            n, m, j = len(s), len(p), 0
            for i in range(n):
                while s[i] != p[j] and j > 0:
                    j = lps[j - 1]
                if s[i] == p[j]:
                    j += 1
                    if j == m: return i - m + 1
            return -1

        return kmp(haystack, needle)
```
