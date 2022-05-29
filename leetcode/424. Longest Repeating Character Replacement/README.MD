# [424. Longest Repeating Character Replacement (Medium)](https://leetcode.com/problems/longest-repeating-character-replacement/)

<p>You are given a string <code>s</code> and an integer <code>k</code>. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most <code>k</code> times.</p>

<p>Return <em>the length of the longest substring containing the same letter you can get after performing the above operations</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "ABAB", k = 2
<strong>Output:</strong> 4
<strong>Explanation:</strong> Replace the two 'A's with two 'B's or vice versa.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "AABABBA", k = 1
<strong>Output:</strong> 4
<strong>Explanation:</strong> Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists of only uppercase English letters.</li>
	<li><code>0 &lt;= k &lt;= s.length</code></li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sliding Window](https://leetcode.com/tag/sliding-window/)

**Similar Questions**:

- [Longest Substring with At Most K Distinct Characters (Medium)](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
- [Max Consecutive Ones III (Medium)](https://leetcode.com/problems/max-consecutive-ones-iii/)
- [Minimum Number of Operations to Make Array Continuous (Hard)](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-continuous/)
- [Maximize the Confusion of an Exam (Medium)](https://leetcode.com/problems/maximize-the-confusion-of-an-exam/)
- [Longest Substring of One Repeating Character (Hard)](https://leetcode.com/problems/longest-substring-of-one-repeating-character/)

## Solution 1. Sliding Window

We build up `count` histogram as we are sliding the window

We keep sliding the window to the right and add the character to `count`

Until we see `numberOfReplacement` go over `k`, then we shrink left

- `numberOfReplacement` is length of the window subtract maximum value in our `count` histogram

- `numberOfReplacement = len(window) - max(count.values) = (hi - lo + 1) - max(count.values())`

```py
# OJ: https://leetcode.com/problems/longest-repeating-character-replacement/
# Author: Duy Tran
# Time: O(N)  O(26N)
# Space: O(1)

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = dict()
        res = 0
        lo, hi = 0, 0
        while hi < len(s):
            c = s[hi]
            count[c] = count.get(c, 0) + 1

            numberOfReplacement = (hi - lo + 1) - max(count.values())
            while numberOfReplacement > k:
                loChar = s[lo]
                count[loChar] -= 1
                lo += 1
                numberOfReplacement = (hi - lo + 1) - max(count.values())

            res = max(res, hi - lo + 1)
            hi += 1
        return res

```

## Solution 2. Sliding Window with Optimization

Our time complexity is O(26 N) which is still O(N), but it is not efficiently.

We have to call `max(count.values()` each time, which is O(26).

We can optimize this by keep track of `maxFreq` that we have ever seen before.

- When sliding right, after update our `count`, we check if we need to update our `maxFreq`

- Why this work? Because we only care our best case, which is the biggest `maxFreq`

```py
# OJ: https://leetcode.com/problems/longest-repeating-character-replacement/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = dict()
        res = 0
        lo, hi = 0, 0
        maxFreq = 0
        while hi < len(s):
            c = s[hi]
            count[c] = count.get(c, 0) + 1
            maxFreq = max(maxFreq, count[c])
            while (hi - lo + 1) - maxFreq > k:
                count[s[lo]] -= 1
                lo += 1
            res = max(res, hi - lo + 1)
            hi += 1
        return res
```
