# [1400. Construct K Palindrome Strings (Medium)](https://leetcode.com/problems/construct-k-palindrome-strings/)

<p>Given a string <code>s</code> and an integer <code>k</code>, return <code>true</code> <em>if you can use all the characters in </em><code>s</code><em> to construct </em><code>k</code><em> palindrome strings or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "annabelle", k = 2
<strong>Output:</strong> true
<strong>Explanation:</strong> You can construct two palindromes using all characters in s.
Some possible constructions "anna" + "elble", "anbna" + "elle", "anellena" + "b"
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "leetcode", k = 3
<strong>Output:</strong> false
<strong>Explanation:</strong> It is impossible to construct 3 palindromes using all the characters of s.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "true", k = 4
<strong>Output:</strong> true
<strong>Explanation:</strong> The only possible solution is to put each character in a separate string.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
	<li><code>1 &lt;= k &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Greedy](https://leetcode.com/tag/greedy/), [Counting](https://leetcode.com/tag/counting/)

## Solution 1. Histogram

Count odd occurrences

Two condition:

1. odd occurrences <= `k`.
2. `k < s.length`. if we have one character in each palindrome, we will have at most `s.length()` palindromes. So we need `k <= s.length()`

Trivial cases:

- k > N, False
- k == N, True

**Example 1:**

For any string with odd character count <= `k` , we can always form `k` palindrome string for sure with `k <= n`

aabb, k=1| abba

aabb, k=2 | aa, bb

aabb, k=3 | a, a, bb

aabb, k=4 | a, a, b, b

**Example 2**:

aabbc, k=1 | aacbb

aabbc, k=2 | aca, bb

aabbc, k=3 | a,a, bcb

aabbc, k=4 | a, a, c ,bb

aabbc, k=5 | a, a, c, b, b

**Example 3:**

aabc, k=1 | N/A

aabc, k=2 | aba, c

aabc, k=3 | aa, b, c

aabc, k=4 | a, a, b, c

```py

# OJ: https://leetcode.com/problems/construct-k-palindrome-strings/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def buildHist(self, s):
        m = defaultdict(int)
        for c in s:
            m[c] += 1
        return dict(m)

    def canConstruct(self, s: str, k: int) -> bool:
        n = len(s)
        if k > n: return False
        if k == n: return True
        hist = self.buildHist(s)
        # count odd frequency
        odd = 0
        for num in hist.values():
            if num % 2 == 1: odd += 1
        return odd <= k

```

## Solution 2. Bit Manipulation

Same concept above, but use bit to keep track of odd occurrences

```py
# OJ: https://leetcode.com/problems/construct-k-palindrome-strings/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def getPos(self, c):
        return 1 << (ord(c) - ord('a'))

    def canConstruct(self, s: str, k: int) -> bool:
        odd = 0
        for c in s:
            odd ^= self.getPos(c)
        return bin(odd).count('1') <= k <= len(s)
```
