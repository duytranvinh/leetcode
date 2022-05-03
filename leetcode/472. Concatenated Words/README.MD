# [472. Concatenated Words (Hard)](https://leetcode.com/problems/concatenated-words/)

<p>Given an array of strings <code>words</code> (<strong>without duplicates</strong>), return <em>all the <strong>concatenated words</strong> in the given list of</em> <code>words</code>.</p>

<p>A <strong>concatenated word</strong> is defined as a string that is comprised entirely of at least two shorter words in the given array.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
<strong>Output:</strong> ["catsdogcats","dogcatsdog","ratcatdogcat"]
<strong>Explanation:</strong> "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
"dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["cat","dog","catdog"]
<strong>Output:</strong> ["catdog"]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= words[i].length &lt;= 30</code></li>
	<li><code>words[i]</code> consists of only lowercase English letters.</li>
	<li><code>0 &lt;= sum(words[i].length) &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Trie](https://leetcode.com/tag/trie/)

**Similar Questions**:

- [Word Break II (Hard)](https://leetcode.com/problems/word-break-ii/)

## Solution 1. DP

[Source](https://github.com/lzl124631x/LeetCode/tree/master/leetcode/472.%20Concatenated%20Words)

```py
# OJ: https://leetcode.com/problems/concatenated-words/
# Author: Duy Tran
# Time: O(N * L^3) where L is the maximum word length.
# Space: O(N or C) where C is the length sum of words.

class Solution:
    def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
        words = set(words)

        def isConcat(s):
            n = len(s)
            dp = [False for _ in range(n)]
            for i in range(n-1):
                # If s[0:i+1] in words, mark dp[i] = true
                if s[0:i+1] in words: dp[i] = True

                # If position i is not reachable, then continue
                if not dp[i]: continue

                # Divide s by half 0 -> i, i+1 -> n
                # Continue search for in the words
                for j in range(i+1, n):
                    # if any part of second half in words => True
                    # 'in' cost O(N)
                    if s[i+1: j+1] in words: dp[j] = True

                # If last index can be reach => True
                if dp[n-1]: return True
            return False
        res = list()
        for w in words:
            if isConcat(w): res.append(w)
        return res

```

## Solution 2. Trie

[Source](https://github.com/lzl124631x/LeetCode/tree/master/leetcode/472.%20Concatenated%20Words)

### Complexity Analysis

Building the Trie will take `O(NW)` time and `O(NW)` space where `N` is the length of `A` and `W` is the maximum word length.

Checking if a word is a concatenated word will take `O(W^2)` time and `O(W)` space. So checking the `N` words will take `O(N * W^2)` time.

So overall, this solution takes `O(N * W^2)` time and `O(NW)` space.

```py
# OJ: https://leetcode.com/problems/concatenated-words/
# Author: Duy Tran
# Time: O(N * L^2)
# Space: O(N*L)

class Trie:
    def __init__(self):
        self.child = defaultdict(Trie)
        self.end = False

    # Add a new word in to Trie
    def addWord(self, word):
        cur = self
        for c in word:
            # defauldict(Trie) helped to create a new Trie if empty
            cur = cur.child[c]
        cur.end = True

class Solution:
    def valid(self, root, s, words):
        n = len(s)
        # dp = [True if reach-able]
        dp = [False for _ in range(n+1)]

        # At first, dp[0] is reachable
        dp[0] = True

        for i in range(n):
            # if that char is not reach-able, skip
            if not dp[i]: continue
            cur = root

            # run from i -> n
            #     except if i == 0, i -> n - 1
            #     avoiding the case where it's itself
            for j in range(i, n - (i == 0)):
                cur = cur.child.get(s[j])
                if cur is None: break
                if cur.end: dp[j+1] = True
                if dp[n]: return True
        return False

    def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
        root = Trie()
        for w in words:
            root.addWord(w)

        res = list()
        for w in words:
            if self.valid(root, w, words): res.append(w)
        return res
```
