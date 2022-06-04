# [130. Surrounded Regions (Medium)](https://leetcode.com/problems/surrounded-regions/)

<p>Given an <code>m x n</code> matrix <code>board</code> containing <code>'X'</code> and <code>'O'</code>, <em>capture all regions that are 4-directionally&nbsp;surrounded by</em> <code>'X'</code>.</p>

<p>A region is <strong>captured</strong> by flipping all <code>'O'</code>s into <code>'X'</code>s in that surrounded region.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg" style="width: 550px; height: 237px;">
<pre><strong>Input:</strong> board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
<strong>Output:</strong> [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
<strong>Explanation:</strong> Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> board = [["X"]]
<strong>Output:</strong> [["X"]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == board.length</code></li>
	<li><code>n == board[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>board[i][j]</code> is <code>'X'</code> or <code>'O'</code>.</li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [tiktok](https://leetcode.com/company/tiktok)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)
- [Walls and Gates (Medium)](https://leetcode.com/problems/walls-and-gates/)

## Solution 1. DFS

Similar to [417. Pacific Atlantic Water Flow](/leetcode/417.%20Pacific%20Atlantic%20Water%20Flow/)

The question asking to eliminate the surrounded area

It also mean only capture the non-surrounded area

Idea:

- Run around the border

- Any connected components with it is a valid `O`

- Otherwise, mark "inside" to be `X`

```py

# OJ: https://leetcode.com/problems/surrounded-regions/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        ROW, COL = len(board), len(board[0])
        visited = [[False for _ in range(COL)] for _ in range(ROW)]
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        def dfs(y, x, visited):
            visited[y][x] = True
            for y1, x1 in dirs:
                dy, dx = y + y1, x + x1
                if dy < 0 or dy == ROW or dx < 0 or dx == COL:  continue
                if board[dy][dx] == 'X':                        continue
                if visited[dy][dx]:                             continue
                dfs(dy, dx, visited)

        for y in range(ROW):
            for x in range(COL):
                if board[y][x] == 'X': continue
                if y == 0 or y == ROW - 1 or x == 0 or x == COL - 1:
                    # Do the DFS here
                    if visited[y][x]: continue
                    dfs(y, x, visited)

        for y in range(ROW):
            for x in range(COL):
                if board[y][x] == 'X': continue
                # The 'O' which is not visited is invalid
                if not visited[y][x]:
                    board[y][x] = 'X'

```

## Solution 2. DFS with Optimization

In the previous solution, we use an extra matrix `visited` to keep track of visited cell

That cost `O(MN)` in term of space complexity

But we can optimize it by using the given `board` itself to mark visited cells

1. (DFS) Capture unsurrounded regions (O -> V)

2. Capture surrounded regions (O -> X)

3. Uncapture unsurrounded regions (V -> O)

The **trade off** is that we have to loop through the board 3 times compare to 2 times in the previous solution

```py
# OJ: https://leetcode.com/problems/surrounded-regions/
# Author: Duy Tran
# Time: O(MN)
# Space: O(1)

class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        ROW, COL = len(board), len(board[0])
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        def dfs(y, x):
            board[y][x] = "V"
            for y1, x1 in dirs:
                dy, dx = y + y1, x + x1
                if dy < 0 or dy == ROW or dx < 0 or dx == COL:  continue
                if board[dy][dx] == 'X':                        continue
                if board[dy][dx] == 'V':                        continue
                dfs(dy, dx)

        # 1. (DFS) Capture unsurrounded regions (O -> V)
        for y in range(ROW):
            for x in range(COL):
                if board[y][x] == 'X': continue
                if board[y][x] == 'V': continue
                if y == 0 or y == ROW - 1 or x == 0 or x == COL - 1:
                    # Do the DFS here
                    dfs(y, x)

        # 2. Capture surrounded regions (O -> X)
        for y in range(ROW):
            for x in range(COL):
                if board[y][x] == "O":
                    board[y][x] = "X"

        # 3. Uncapture unsurrounded regions (V -> O)
        for y in range(ROW):
            for x in range(COL):
                if board[y][x] == "V":
                    board[y][x] = "O"
```
