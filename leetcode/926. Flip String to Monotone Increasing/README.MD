# [926. Flip String to Monotone Increasing (Medium)](https://leetcode.com/problems/flip-string-to-monotone-increasing/)

<p>A binary string is monotone increasing if it consists of some number of <code>0</code>'s (possibly none), followed by some number of <code>1</code>'s (also possibly none).</p>

<p>You are given a binary string <code>s</code>. You can flip <code>s[i]</code> changing it from <code>0</code> to <code>1</code> or from <code>1</code> to <code>0</code>.</p>

<p>Return <em>the minimum number of flips to make </em><code>s</code><em> monotone increasing</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "00110"
<strong>Output:</strong> 1
<strong>Explanation:</strong> We flip the last digit to get 00111.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "010110"
<strong>Output:</strong> 2
<strong>Explanation:</strong> We flip to get 011111, or alternatively 000111.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "00011000"
<strong>Output:</strong> 2
<strong>Explanation:</strong> We flip to get 00000000.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s[i]</code> is either <code>'0'</code> or <code>'1'</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

## Solution 1. Two Passes

Initial: Flip all 0, make it into all 1

Loop: If `0`, the reduce the flip of `0` by 1. If `1`, increasing the flip of `1` by 1

Basically, we loop through all scenarios

Find min of total flip of each iteration/scenario

```
   00110
0: 3 1: 0 total: 3
0: 2 1: 0 total: 2
0: 1 1: 0 total: 1
0: 1 1: 1 total: 2
0: 1 1: 2 total: 3
0: 0 1: 2 total: 2
```

```py
# OJ: https://leetcode.com/problems/flip-string-to-monotone-increasing/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def minFlipsMonoIncr(self, s: str) -> int:
        right0, left1 = s.count('0'), 0
        res = right0
        for c in s:
            if c == '1': left1 += 1
            else: right0 -= 1
            res = min(res, right0 + left1)
        return res

```

## Solution 2. One Pass (DP)

Think it is DP problem. Assume we've already solved the sub-problem for substring `s[0..i]`, and the solution for it is `flipCount[i]`.

Then we look at next one `s[i+1]`:

- If it's `1`, then we can reuse our previous solution so `flipCount[i + 1] = flipCount[i]`.
  - Why? Because our `i` is increasing
  - So if it's `1` then we can assume on the right side of the `s`
  - So we don't need to do anything more, just reuse old solution ` flipCount[i]`
- If it's `0`, then we have to consider two case:
  1. We can choose to flip this `0` to `1` and reuse the solution for `s[0..i]`. In this case `flipCount[i + 1] = flipCount[i] + 1`.
  2. What if the best solution is not to flip? Then we need to turn all `1`s in `s[0..i]` into `0`. Assume the count of `1`s in `s[0..i]` is `ones[i]`, then `flipCount[i + 1] = ones[i]`
- At each iteration `s[i+1]`, we keep track of our final solution by using `min()`
  - If it's `1`, then `flipCount[i+1] = min(flipCount[i], ones[i]) = flipCount[i]`
  - If it's `0`, then `flipCount[i+1] = min(flipCount[i] + 1, ones[i])`

We don't need the whole `DP` /` flipCount` since we only use the previous solution, therefore we can use `prev` / `flip` to keep track of the previous solution

We can use `cnt` to keep track all `1`s so far at `ones[i]`

```py
# OJ: https://leetcode.com/problems/flip-string-to-monotone-increasing/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)
# Ref: https://github.com/lzl124631x/LeetCode/tree/master/leetcode/926.%20Flip%20String%20to%20Monotone%20Increasing

class Solution:
    def minFlipsMonoIncr(self, s: str) -> int:
        cnt, flip = 0, 0
        for c in s:
            if c == '1': cnt += 1
            else:        flip += 1
            flip = min(flip, cnt)
        return flip
```
