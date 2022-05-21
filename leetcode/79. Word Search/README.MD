# [79. Word Search (Medium)](https://leetcode.com/problems/word-search/)

<p>Given an <code>m x n</code> grid of characters <code>board</code> and a string <code>word</code>, return <code>true</code> <em>if</em> <code>word</code> <em>exists in the grid</em>.</p>

<p>The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word2.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
<strong>Output:</strong> true
</pre>

<p><strong>Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/15/word3.jpg" style="width: 322px; height: 242px;">
<pre><strong>Input:</strong> board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n = board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 6</code></li>
	<li><code>1 &lt;= word.length &lt;= 15</code></li>
	<li><code>board</code> and <code>word</code> consists of only lowercase and uppercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you use search pruning to make your solution faster with a larger <code>board</code>?</p>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Twitter](https://leetcode.com/company/twitter), [Microsoft](https://leetcode.com/company/microsoft), [Karat](https://leetcode.com/company/karat), [Uber](https://leetcode.com/company/uber), [Bloomberg](https://leetcode.com/company/bloomberg), [Facebook](https://leetcode.com/company/facebook), [Indeed](https://leetcode.com/company/indeed), [Cisco](https://leetcode.com/company/cisco), [tiktok](https://leetcode.com/company/tiktok), [Snapchat](https://leetcode.com/company/snapchat), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Wayfair](https://leetcode.com/company/wayfair), [Samsung](https://leetcode.com/company/samsung), [Roblox](https://leetcode.com/company/roblox), [Bolt](https://leetcode.com/company/bolt)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Backtracking](https://leetcode.com/tag/backtracking/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Word Search II (Hard)](https://leetcode.com/problems/word-search-ii/)

## Solution 1. Backtracking, DFS

Starting at a valid `word[0]`

Then DFS/Backtracking to four different directions

**Time Complexity**

O(N\*M) to search through the map

Since we going 4 direction, it's O(4^K), where K = `len(s)`

So total is O(N*M * 4^K)

**Space Complexity**

O(N\*M) for storing visited array

But we can save this by mark visited into our `board`

Make this become O(K), to store all the characters in `word`

```py
# OJ: https://leetcode.com/problems/word-search/
# Author: Duy Tran
# Time: O(N*M * 4^K)
# Space: O(N*M)

class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        n = len(board)
        m = len(board[0]) if n else 0
        visited = set()
        dirs = [[0,1], [1,0], [0,-1], [-1, 0]] # top,right,bot,left
        def dfs(i, j, index):
            if index == len(word):
                return True
            if i < 0 or i >= n or j < 0 or j >= m:  return False
            if board[i][j] != word[index]:          return False
            if (i, j) in visited:                   return False
            visited.add((i, j))
            for dx, dy in dirs:
                if dfs(i + dx, j + dy, index + 1):
                    return True
            visited.remove((i, j))
            return False
        for i in range(n):
            for j in range(m):
                if board[i][j] != word[0]: continue
                if dfs(i, j, 0): return True

```
