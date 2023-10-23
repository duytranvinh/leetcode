# [140. Word Break II (Hard)](https://leetcode.com/problems/word-break-ii/)

<p>Given a string <code>s</code> and a dictionary of strings <code>wordDict</code>, add spaces in <code>s</code> to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in <strong>any order</strong>.</p>

<p><strong>Note</strong> that the same word in the dictionary may be reused multiple times in the segmentation.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
<strong>Output:</strong> ["cats and dog","cat sand dog"]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "pineapplepenapple", wordDict = ["apple","pen","applepen","pine","pineapple"]
<strong>Output:</strong> ["pine apple pen apple","pineapple pen apple","pine applepen apple"]
<strong>Explanation:</strong> Note that you are allowed to reuse a dictionary word.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 20</code></li>
	<li><code>1 &lt;= wordDict.length &lt;= 1000</code></li>
	<li><code>1 &lt;= wordDict[i].length &lt;= 10</code></li>
	<li><code>s</code> and <code>wordDict[i]</code> consist of only lowercase English letters.</li>
	<li>All the strings of <code>wordDict</code> are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Microsoft](https://leetcode.com/company/microsoft), [Snapchat](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Backtracking](https://leetcode.com/tag/backtracking/), [Trie](https://leetcode.com/tag/trie/), [Memoization](https://leetcode.com/tag/memoization/)

**Similar Questions**:

- [Word Break (Medium)](https://leetcode.com/problems/word-break/)
- [Concatenated Words (Hard)](https://leetcode.com/problems/concatenated-words/)

## Solution 1. Backtracking

Use `dp[i]` to keep track whether `i` will go to the or not
`dp = [-1 for unvisited, 1 for success reaching end, 0 for failure]`
Search every word in `s` to see if it's in the `wordDict`

```py
# OJ: https://leetcode.com/problems/word-break-ii/
# Author: Duy Tran
# Time: O(2^n) and n is length of string
# Space: O(N + M) n is the length of string, and m is length of the 'wordDict'
# Ref: https://github.com/lzl124631x/LeetCode/tree/master/leetcode/140.%20Word%20Break%20II

class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        wDict = set(wordDict)
        res = list()
        path = list()
        n = len(s)
        dp = [False for _ in range(n + 1)]
        dp[n] = 1
        def dfs(st, i):
            # end path
            if i == n:
                tmp = str()
                for w in path:
                    tmp += (' ' if len(tmp) else '') + w
                res.append(tmp)

            # backtracking every possible path
            for j in range(i + 1, n + 1):
                sub = st[i:j]
                if sub not in wDict: continue
                path.append(sub)
                dfs(st, j)
                path.pop()
            
        dfs(s, 0)
        return res
```

Javascript

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {string[]}
 */
var wordBreak = function(s, wordDict) {
    const wDict = new Set(wordDict);
    const res = new Array();
    const path = new Array();
    const n = s.length;
    const dfs = (st, i) => {
        if (i === n) {
            let tmp = new String();
            for (const w of path) {
                tmp += (tmp.length ? " " : "") + w
            }
            res.push(tmp);
        }
        for (var j = i + 1; j <= n; j++) {
            const sub = st.substring(i, j);
            if (!wDict.has(sub)) continue;
            path.push(sub);
            dfs(st, j)
            path.pop();
        }
    }
    dfs(s, 0);
    return res;
};
```

## Solution 2. Backtracking + Memoization

Might not sufficient to find a solution

Keep track the path that is used

```py

# OJ: https://leetcode.com/problems/word-break-ii/
# Author: Duy Tran
# Time: O(N!)
# Space: O(N + D)
# Ref: https://leetcode.com/problems/word-break-ii/discuss/44167/My-concise-JAVA-solution-based-on-memorized-DFS

class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        m = dict()

        def dfs(s):
            if s in m:
                return m[s]

            res = list()
            if len(s) == 0:
                res.append('')
                return res

            for word in wordDict:
                if s.startswith(word):
                    l = len(word)
                    subList = dfs(s[l:])
                    for sub in subList:
                        r = (word) + (" " if sub else '') + (sub)
                        res.append(r)
            m[s] = res
            return res

        return dfs(s)
```
