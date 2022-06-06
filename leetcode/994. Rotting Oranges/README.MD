# [994. Rotting Oranges (Medium)](https://leetcode.com/problems/rotting-oranges/)

<p>You are given an <code>m x n</code> <code>grid</code> where each cell can have one of three values:</p>

<ul>
	<li><code>0</code> representing an empty cell,</li>
	<li><code>1</code> representing a fresh orange, or</li>
	<li><code>2</code> representing a rotten orange.</li>
</ul>

<p>Every minute, any fresh orange that is <strong>4-directionally adjacent</strong> to a rotten orange becomes rotten.</p>

<p>Return <em>the minimum number of minutes that must elapse until no cell has a fresh orange</em>. If <em>this is impossible, return</em> <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/02/16/oranges.png" style="width: 650px; height: 137px;">
<pre><strong>Input:</strong> grid = [[2,1,1],[1,1,0],[0,1,1]]
<strong>Output:</strong> 4
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[2,1,1],[0,1,1],[1,0,1]]
<strong>Output:</strong> -1
<strong>Explanation:</strong> The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> grid = [[0,2]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> Since there are already no fresh oranges at minute 0, the answer is just 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10</code></li>
	<li><code>grid[i][j]</code> is <code>0</code>, <code>1</code>, or <code>2</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [VMware](https://leetcode.com/company/vmware), [LinkedIn](https://leetcode.com/company/linkedin)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Walls and Gates (Medium)](https://leetcode.com/problems/walls-and-gates/)
- [Detonate the Maximum Bombs (Medium)](https://leetcode.com/problems/detonate-the-maximum-bombs/)
- [Escape the Spreading Fire (Hard)](https://leetcode.com/problems/escape-the-spreading-fire/)

## Solution 1. BFS

BFS through all of the rotten oranges

At first, we count all `fresh` oranges, and put `rotten` oranges into our `q`

Then we do BFS for our `q`.

At the end, if `fresh == 0` then we return our time. Otherwise, we return `-1`

```py

# OJ: https://leetcode.com/problems/rotting-oranges/
# Author: Duy Tran
# Time: O(N), N is the size of the grid
# Space: O(N)

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        ROW, COL = len(grid), len(grid[0])
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        fresh, time = 0, 0
        q = collections.deque()

        for y in range(ROW):
            for x in range(COL):
                if grid[y][x] == 0: continue
                if grid[y][x] == 1:
                    fresh += 1
                else:
                    q.append((y, x))

        while q and fresh > 0:
            rotted = len(q)
            for _ in range(rotted):
                y, x = q.popleft()
                for y1, x1 in dirs:
                    dy, dx = y + y1, x + x1
                    if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue
                    # if grid[dy][dx] == 0:                           continue
                    # if grid[dy][dx] == 2:                           continue
                    if grid[dy][dx] != 1:                           continue
                    grid[dy][dx] = 2
                    q.append((dy,dx))
                    fresh -= 1
            time += 1

        return time if fresh == 0 else -1

```
