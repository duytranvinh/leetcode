# [76. Minimum Window Substring (Hard)](https://leetcode.com/problems/minimum-window-substring/)

<p>Given two strings <code>s</code> and <code>t</code> of lengths <code>m</code> and <code>n</code> respectively, return <em>the <strong>minimum window substring</strong> of </em><code>s</code><em> such that every character in </em><code>t</code><em> (<strong>including duplicates</strong>) is included in the window. If there is no such substring</em><em>, return the empty string </em><code>""</code><em>.</em></p>

<p>The testcases will be generated such that the answer is <strong>unique</strong>.</p>

<p>A <strong>substring</strong> is a contiguous sequence of characters within the string.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "ADOBECODEBANC", t = "ABC"
<strong>Output:</strong> "BANC"
<strong>Explanation:</strong> The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "a", t = "a"
<strong>Output:</strong> "a"
<strong>Explanation:</strong> The entire string s is the minimum window.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "a", t = "aa"
<strong>Output:</strong> ""
<strong>Explanation:</strong> Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == s.length</code></li>
	<li><code>n == t.length</code></li>
	<li><code>1 &lt;= m, n&nbsp;&lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> and <code>t</code> consist of uppercase and lowercase English letters.</li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you find an algorithm that runs in <code>O(m + n)</code> time?

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [LinkedIn](https://leetcode.com/company/linkedin), [Microsoft](https://leetcode.com/company/microsoft), [Lyft](https://leetcode.com/company/lyft), [Airbnb](https://leetcode.com/company/airbnb), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Snapchat](https://leetcode.com/company/snapchat), [Oracle](https://leetcode.com/company/oracle), [Nagarro](https://leetcode.com/company/nagarro)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sliding Window](https://leetcode.com/tag/sliding-window/)

**Similar Questions**:

- [Substring with Concatenation of All Words (Hard)](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
- [Minimum Size Subarray Sum (Medium)](https://leetcode.com/problems/minimum-size-subarray-sum/)
- [Sliding Window Maximum (Hard)](https://leetcode.com/problems/sliding-window-maximum/)
- [Permutation in String (Medium)](https://leetcode.com/problems/permutation-in-string/)
- [Smallest Range Covering Elements from K Lists (Hard)](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)
- [Minimum Window Subsequence (Hard)](https://leetcode.com/problems/minimum-window-subsequence/)

## Solution 1. Sliding Window

At first, we build Histogram for `t` as `countT`

We keep track `have, need = 0, len(countT)`

Then we slide window to build up Histogram for `s` as `window`

To save space for our `window`, only need to add `c` that appear in `countT`

If `window[c] == countT[c]`, then we update our `have`

When we reach `have == need`, we shrink our left side:

- Update result. Find the minimum window

- Shrink left. Remove character from `window` if needed and update our `lo`

```py
# OJ: https://leetcode.com/problems/minimum-window-substring/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if len(t) == 0 or len(t) > len(s):
            return ""

        countT, window = dict(), dict()

        for c in t:
            countT[c] = countT.get(c, 0) + 1

        have, need = 0, len(countT)
        res, resLen = [-1, -1], float("infinity")
        lo, hi = 0, 0

        while hi < len(s):

            c = s[hi]
            if c in countT:
                window[c] = window.get(c, 0) + 1
                if window[c] == countT[c]: have += 1

            # We shrinking until it's unvalid
            while have == need:
                # update result
                if (hi - lo + 1) < resLen:
                    res = [lo, hi]
                    resLen = (hi - lo + 1)

                # shrink left
                charLo = s[lo]
                if charLo in countT:
                    window[charLo] -= 1
                    if window[charLo] < countT[charLo]: have -= 1

                lo += 1

            hi += 1

        lo, hi = res
        return s[lo: hi + 1] if resLen != float("infinity") else ""


```
