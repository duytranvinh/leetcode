# [438. Find All Anagrams in a String (Medium)](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

<p>Given two strings <code>s</code> and <code>p</code>, return <em>an array of all the start indices of </em><code>p</code><em>'s anagrams in </em><code>s</code>. You may return the answer in <strong>any order</strong>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "cbaebabacd", p = "abc"
<strong>Output:</strong> [0,6]
<strong>Explanation:</strong>
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "abab", p = "ab"
<strong>Output:</strong> [0,1,2]
<strong>Explanation:</strong>
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length, p.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>s</code> and <code>p</code> consist of lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Yahoo](https://leetcode.com/company/yahoo), [Oracle](https://leetcode.com/company/oracle), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Bolt](https://leetcode.com/company/bolt)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sliding Window](https://leetcode.com/tag/sliding-window/)

**Similar Questions**:

- [Valid Anagram (Easy)](https://leetcode.com/problems/valid-anagram/)
- [Permutation in String (Medium)](https://leetcode.com/problems/permutation-in-string/)

## Solution 1. Sliding Window

At first, we build our `pCount` histogram

Then we we build our `sCount` histogram as we sliding

Everytime we slide the window to the right, we add the character into `sCount`

Everytime we shrink left side, we subtract it from our `sCount`. If `sCount[c] == 0`, then we remove that character

At anytime, if `sCount == pCount`, we at that `left` position into our result

`sCount == pCount` will cost O(R) where R is the range of characters, which is at max 26 English characters, which is O(1)

```py

# OJ: https://leetcode.com/problems/find-all-anagrams-in-a-string/
# Author: Duy Tran
# Time: O(M + RN) where `R` is the range of characters
# Space: O(1)

class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        n, m = len(s), len(p)
        if m > n: return []

        pCount, sCount = dict(), dict()
        for i in range(m):
            pCount[p[i]] = pCount.get(p[i], 0) + 1
            sCount[s[i]] = sCount.get(s[i], 0) + 1

        l, r = 0, m
        res = list()
        if sCount == pCount: res.append(l)

        while r < n:
            charL, charR = s[l], s[r]
            sCount[charR] = sCount.get(charR, 0) + 1
            sCount[charL] -= 1

            if sCount[charL] == 0:
                sCount.pop(charL)

            r += 1
            l += 1
            if sCount == pCount: #this cost O(M or N), which is O(26) at max
                res.append(l)

        return res

```

## Solution 2. Sliding Window with Optimization

We can see that we have to search through the `pCount` and `sCount` multiple times and that's costly to do

We can optimize it more by keep track of the `matched` character

How can we keep track of this?

At first, we build up our `pCount` histogram

Then we loop/sliding through our main string `s`

Every time we see a new character, we subtract it from our `pCount`

Every time we shrink left, we add it back it our `pCount`

Eventually, as we were initial our `pCount` before we loop `s`, therefore, only valid characters that will have a positive count [-infinity, infinity]

Those are invalid, will be at max 0. [-infinity, 0]

Therefore, if `pCount[c] > 0: matched++`, and if `pCount[charL] > 0: matched -= 1`

At any given time, if `matched == p.length`, then we add our left side to the result

```py
# OJ: https://leetcode.com/problems/find-all-anagrams-in-a-string/
# Author: Duy Tran
# Time: O(M + N)
# Space: O(1), O(26)

class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        n, m = len(s), len(p)
        pCount = defaultdict(int)
        for c in p:
            pCount[c] += 1
        matched = 0
        res = list()
        charL = str()
        for i in range(n):
            c = s[i]
            pCount[c] -= 1

            if pCount[c] >= 0:
                matched += 1

            if i >= m:
                charL = s[i - m]
                pCount[charL] += 1
                if pCount[charL] > 0: matched -= 1

            if matched == m:
                res.append(i - m + 1)
            # print(matched, c, charL, dict(pCount))

        return res
```
