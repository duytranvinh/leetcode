# [3. Longest Substring Without Repeating Characters (Medium)](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

<p>Given a string <code>s</code>, find the length of the <strong>longest substring</strong> without repeating characters.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "abcabcbb"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The answer is "abc", with the length of 3.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "bbbbb"
<strong>Output:</strong> 1
<strong>Explanation:</strong> The answer is "b", with the length of 1.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "pwwkew"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code> consists of English letters, digits, symbols and spaces.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Spotify](https://leetcode.com/company/spotify), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [VMware](https://leetcode.com/company/vmware), [Oracle](https://leetcode.com/company/oracle), [Yahoo](https://leetcode.com/company/yahoo), [Intuit](https://leetcode.com/company/intuit), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [Salesforce](https://leetcode.com/company/salesforce), [Zoho](https://leetcode.com/company/zoho), [Paypal](https://leetcode.com/company/paypal), [Expedia](https://leetcode.com/company/expedia), [Yandex](https://leetcode.com/company/yandex)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Sliding Window](https://leetcode.com/tag/sliding-window/)

**Similar Questions**:

- [Longest Substring with At Most Two Distinct Characters (Medium)](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
- [Longest Substring with At Most K Distinct Characters (Medium)](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
- [Subarrays with K Different Integers (Hard)](https://leetcode.com/problems/subarrays-with-k-different-integers/)
- [Maximum Erasure Value (Medium)](https://leetcode.com/problems/maximum-erasure-value/)
- [Number of Equal Count Substrings (Medium)](https://leetcode.com/problems/number-of-equal-count-substrings/)
- [Minimum Consecutive Cards to Pick Up (Medium)](https://leetcode.com/problems/minimum-consecutive-cards-to-pick-up/)

## Solution 1. Sliding Window

More about sliding windows templates [here](https://leetcode.com/problems/frequency-of-the-most-frequent-element/discuss/1175088/C%2B%2B-Maximum-Sliding-Window-Cheatsheet-Template!)

Shrinkable Sliding Window:

```cpp
int i = 0, j = 0, ans = 0;
for (; j < N; ++j) {
    // CODE: use A[j] to update state which might make the window invalid
    for (; invalid(); ++i) { // when invalid, keep shrinking the left edge until it's valid again
        // CODE: update state using A[i]
    }
    ans = max(ans, j - i + 1); // the window [i, j] is the maximum window we've found thus far
}
return ans;
```

In this problem, we use Set() to keep track of the character that is used

```py
# OJ: https://leetcode.com/problems/longest-substring-without-repeating-characters/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        charSet = set()
        lo, hi = 0, 0
        res = 0
        while hi < len(s):
            while s[hi] in charSet:
                charSet.remove(s[lo])
                lo += 1
            charSet.add(s[hi])
            res = max(res, hi - lo + 1)
            hi += 1
        return res


```
