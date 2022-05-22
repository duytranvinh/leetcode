# [212. Word Search II (Hard)](https://leetcode.com/problems/word-search-ii/)

<p>Given an <code>m x n</code> <code>board</code>&nbsp;of characters and a list of strings <code>words</code>, return <em>all words on the board</em>.</p>

<p>Each word must be constructed from letters of sequentially adjacent cells, where <strong>adjacent cells</strong> are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/07/search1.jpg" style="width: 322px; height: 322px;">
<pre><strong>Input:</strong> board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
<strong>Output:</strong> ["eat","oath"]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/07/search2.jpg" style="width: 162px; height: 162px;">
<pre><strong>Input:</strong> board = [["a","b"],["c","d"]], words = ["abcb"]
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 12</code></li>
	<li><code>board[i][j]</code> is a lowercase English letter.</li>
	<li><code>1 &lt;= words.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= words[i].length &lt;= 10</code></li>
	<li><code>words[i]</code> consists of lowercase English letters.</li>
	<li>All the strings of <code>words</code> are unique.</li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Amazon](https://leetcode.com/company/amazon), [Cisco](https://leetcode.com/company/cisco), [Microsoft](https://leetcode.com/company/microsoft), [Karat](https://leetcode.com/company/karat), [Facebook](https://leetcode.com/company/facebook), [Snapchat](https://leetcode.com/company/snapchat), [Google](https://leetcode.com/company/google), [Twitter](https://leetcode.com/company/twitter), [Apple](https://leetcode.com/company/apple), [Indeed](https://leetcode.com/company/indeed), [tiktok](https://leetcode.com/company/tiktok), [Qualtrics](https://leetcode.com/company/qualtrics)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Backtracking](https://leetcode.com/tag/backtracking/), [Trie](https://leetcode.com/tag/trie/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Word Search (Medium)](https://leetcode.com/problems/word-search/)
- [Unique Paths III (Hard)](https://leetcode.com/problems/unique-paths-iii/)
- [Encrypt and Decrypt Strings (Hard)](https://leetcode.com/problems/encrypt-and-decrypt-strings/)

## Solution 1. Trie + DFS (Backtracking)

[Reference](https://github.com/lzl124631x/LeetCode/tree/master/leetcode/212.%20Word%20Search%20II)

Look at [Word Search](/leetcode/79.%20Word%20Search/) for a single word backtracking

Build a Trie for each word in the word list

Backtracking for each word that match the tree

Mark `isWord` to False when the word is found, prevent multiple words. But this is still Time Limit

**Optimization**

Use `count` to keep track of each character in `word`, if the `word` is found, we don't need to run through that path again

```py
# OJ: https://leetcode.com/problems/word-search-ii/
# Author: Duy Tran
# Time: O(WL + MN * 4^L) where M, N is the size of board, W is the size of words and L is the average length of word
# Space: O(WL)

class TrieNode:
    def __init__(self):
        self.children = defaultdict(TrieNode)
        self.count = 0
        self.isWord = False

    def addWord(self, word):
        cur = self
        for c in word:
            cur = cur.children[c]
            cur.count += 1
        cur.isWord = True

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        root = TrieNode()

        for w in words:
            root.addWord(w)

        n = len(board)
        m = len(board[0]) if n else 0
        visited = set()
        dirs = [[0,1], [1,0], [0,-1], [-1, 0]] # top,right,bot,left
        res = list()

        def dfs(node, i, j, word):
            # if i < 0 or i >= n or j < 0 or j >= m:  return
            c = board[i][j]
            count = 0
            if c not in node.children or node.children[c].count == 0:  return 0
            visited.add((i, j))
            node = node.children[c]
            word += c
            if node.isWord:
                res.append(word)
                node.isWord = False
                count += 1

            for dx, dy in dirs:
                a = i + dx
                b = j + dy
                if a < 0 or a >= n or b < 0 or b >= m:  continue
                if (a, b) in visited: continue
                count += dfs(node, a, b, word)

            visited.remove((i, j))
            node.count -= count
            return count


        for i in range(n):
            for j in range(m):
                c = board[i][j]
                if c not in root.children: continue
                dfs(root, i, j, '')

        return res

```
