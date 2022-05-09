# [696. Count Binary Substrings (Easy)](https://leetcode.com/problems/count-binary-substrings/)

<p>Give a binary string <code>s</code>, return the number of non-empty substrings that have the same number of <code>0</code>'s and <code>1</code>'s, and all the <code>0</code>'s and all the <code>1</code>'s in these substrings are grouped consecutively.</p>

<p>Substrings that occur multiple times are counted the number of times they occur.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "00110011"
<strong>Output:</strong> 6
<strong>Explanation:</strong> There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".
Notice that some of these substrings repeat and are counted the number of times they occur.
Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "10101"
<strong>Output:</strong> 4
<strong>Explanation:</strong> There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s[i]</code> is either <code>'0'</code> or <code>'1'</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [tiktok](https://leetcode.com/company/tiktok), [Nvidia](https://leetcode.com/company/nvidia), [Myntra](https://leetcode.com/company/myntra), [Oracle](https://leetcode.com/company/oracle)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:

- [Encode and Decode Strings (Medium)](https://leetcode.com/problems/encode-and-decode-strings/)

## Solution 1.

What's a `group` means?

A `group` is either 0s or 1s (`000` or `111`)

We want two `group` consecutively `000111`

With `000111`, we have 3 valid answer `000111`, `0011`, `01`

With `0011111`, we have 2 valid answer `0011`, `01`

We notice that we need to find `min(group0, group1)`

We count each group consecutively and then we find `min` then we reset for the next groups

Loop:

- If the same char, then increase `curGroup`
- If different char, then we find `min`, swap `prevGroup = curGroup` and `curGroup = 1`

Since our loop stop at `N`, so we to add our answer of the last pair of groups to our `res`

```py
# OJ: https://leetcode.com/problems/count-binary-substrings/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def countBinarySubstrings(self, s: str) -> int:
        n = len(s)
        prev, cur = 0, 1
        res = 0
        for i in range(1, n):
            if s[i] == s[i - 1]:
                cur += 1
            else:
                res += min(prev, cur)
                prev = cur
                cur = 1
        return res + min(prev, cur)
```
