# [139. Word Break (Medium)](https://leetcode.com/problems/word-break/)

<p>Given a string <code>s</code> and a dictionary of strings <code>wordDict</code>, return <code>true</code> if <code>s</code> can be segmented into a space-separated sequence of one or more dictionary words.</p>

<p><strong>Note</strong> that the same word in the dictionary may be reused multiple times in the segmentation.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "leetcode", wordDict = ["leet","code"]
<strong>Output:</strong> true
<strong>Explanation:</strong> Return true because "leetcode" can be segmented as "leet code".
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "applepenapple", wordDict = ["apple","pen"]
<strong>Output:</strong> true
<strong>Explanation:</strong> Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 300</code></li>
	<li><code>1 &lt;= wordDict.length &lt;= 1000</code></li>
	<li><code>1 &lt;= wordDict[i].length &lt;= 20</code></li>
	<li><code>s</code> and <code>wordDict[i]</code> consist of only lowercase English letters.</li>
	<li>All the strings of <code>wordDict</code> are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Qualtrics](https://leetcode.com/company/qualtrics), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Oracle](https://leetcode.com/company/oracle), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [tiktok](https://leetcode.com/company/tiktok)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Trie](https://leetcode.com/tag/trie/), [Memoization](https://leetcode.com/tag/memoization/)

**Similar Questions**:

- [Word Break II (Hard)](https://leetcode.com/problems/word-break-ii/)

## Solution 1. DP Bottom Up

```
Initial the arr of False with size n + 1
Setup buffer with arr[n] = True
Run Bottom Up of the string
  For each index, check every word in the wordDict
    For each word, check if it fit into the string
      dp[i] = dp[i + len(w)]
      (dp[i + len(w)] because we need at that index, it's break-able)
Return dp[0]
```

```py
# OJ: https://leetcode.com/problems/word-break/
# Author: Duy Tran
# Time: O(N * M * N <=> N**2*M <=> N**3)
# Space: O(N)

class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        n = len(s)
        m = len(wordDict)
        dp = [False for _ in range(n + 1)]
        # Setup buffer at "out of bound" index
        dp[n] = True

        # run bottom-up, backward of the string
        for i in range(n - 1, -1, -1):
            # at each index
            # check if w is fit into s
            for w in wordDict:
                l = len(w) + i
                if l <= n and s[i:l] == w:
                    # at index i, there's a potential break
                    # at index L, is there breakable?
                    # True, s[i:l] and s[l:n] is break-able in wordDict
                    # False if s[l:n] is not break-able
                    dp[i] = dp[l]
                if dp[i]: break

        return dp[0]
```
