# [1888. Minimum Number of Flips to Make the Binary String Alternating (Medium)](https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/)

<p>You are given a binary string <code>s</code>. You are allowed to perform two types of operations on the string in any sequence:</p>

<ul>
	<li><strong>Type-1: Remove</strong> the character at the start of the string <code>s</code> and <strong>append</strong> it to the end of the string.</li>
	<li><strong>Type-2: Pick</strong> any character in <code>s</code> and <strong>flip</strong> its value, i.e., if its value is <code>'0'</code> it becomes <code>'1'</code> and vice-versa.</li>
</ul>

<p>Return <em>the <strong>minimum</strong> number of <strong>type-2</strong> operations you need to perform</em> <em>such that </em><code>s</code> <em>becomes <strong>alternating</strong>.</em></p>

<p>The string is called <strong>alternating</strong> if no two adjacent characters are equal.</p>

<ul>
	<li>For example, the strings <code>"010"</code> and <code>"1010"</code> are alternating, while the string <code>"0100"</code> is not.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "111000"
<strong>Output:</strong> 2
<strong>Explanation</strong>: Use the first operation two times to make s = "100011".
Then, use the second operation on the third and sixth elements to make s = "10<u>1</u>01<u>0</u>".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "010"
<strong>Output:</strong> 0
<strong>Explanation</strong>: The string is already alternating.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "1110"
<strong>Output:</strong> 1
<strong>Explanation</strong>: Use the second operation on the second element to make s = "1<u>0</u>10".
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s[i]</code> is either <code>'0'</code> or <code>'1'</code>.</li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Greedy](https://leetcode.com/tag/greedy/)

**Similar Questions**:

- [Minimum Operations to Make the Array Alternating (Medium)](https://leetcode.com/problems/minimum-operations-to-make-the-array-alternating/)

## Solution 1. Sliding Window

Given string `1100`

There are only two possible solutions: `1010` or `0101`

Our job is to count the minimum number of flip we need to make it into the solutions

Our Type-1 operation allow us to cyclic the string. Therefore, we can simulate the string by `s = s + s`

Then we do sliding window to the right. We check the difference of our `s` to our `target`s

We shrink left when `window.length > n`. As we shrinking, we remove the left side of difference.

We only keep minimum number of flip we need to make for our `res`

Building target string. This cost O(2N) = O(N) in term of time and space

```py
s = s + s
atl1, atl2 = "", ""
for i in range(len(s)):
    atl1 += "0" if i % 2 else "1"
    atl2 += "1" if i % 2 else "0"
```

```py
# OJ: https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def minFlips(self, s: str) -> int:
        n = len(s)
        s = s + s
        atl1, atl2 = "", ""
        for i in range(len(s)):
            atl1 += "0" if i % 2 else "1"
            atl2 += "1" if i % 2 else "0"

        res = len(s)
        diff1, diff2 = 0, 0
        l, r = 0, 0

        while r < len(s):
            if s[r] != atl1[r]:
                diff1 += 1
            if s[r] != atl2[r]:
                diff2 += 1

            if (r - l + 1) > n:
                if s[l] != atl1[l]:
                    diff1 -= 1
                if s[l] != atl2[l]:
                    diff2 -= 1
                l += 1

            if (r - l + 1) == n:
                res = min(res, diff1, diff2)

            r += 1

        return res
```

## Solution 2. Sliding Window with optimization
