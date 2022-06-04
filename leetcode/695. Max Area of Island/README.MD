# [695. Max Area of Island (Medium)](https://leetcode.com/problems/max-area-of-island/)

<p>You are given an <code>m x n</code> binary matrix <code>grid</code>. An island is a group of <code>1</code>'s (representing land) connected <strong>4-directionally</strong> (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.</p>

<p>The <strong>area</strong> of an island is the number of cells with a value <code>1</code> in the island.</p>

<p>Return <em>the maximum <strong>area</strong> of an island in </em><code>grid</code>. If there is no island, return <code>0</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg" style="width: 500px; height: 310px;">
<pre><strong>Input:</strong> grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The answer is not 11, because the island must be connected 4-directionally.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[0,0,0,0,0,0,0,0]]
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 50</code></li>
	<li><code>grid[i][j]</code> is either <code>0</code> or <code>1</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [LinkedIn](https://leetcode.com/company/linkedin), [Qualtrics](https://leetcode.com/company/qualtrics), [Apple](https://leetcode.com/company/apple), [Dropbox](https://leetcode.com/company/dropbox), [DoorDash](https://leetcode.com/company/doordash), [Oracle](https://leetcode.com/company/oracle), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [Palantir Technologies](https://leetcode.com/company/palantir-technologies)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)
- [Island Perimeter (Easy)](https://leetcode.com/problems/island-perimeter/)
- [Largest Submatrix With Rearrangements (Medium)](https://leetcode.com/problems/largest-submatrix-with-rearrangements/)
- [Detonate the Maximum Bombs (Medium)](https://leetcode.com/problems/detonate-the-maximum-bombs/)

## Solution 1. BFS

We BFS through the grid.

Every island found, we sink them so it won't be duplicated.

Return the area for each island found

Then we keep track of the highest area

```py
# OJ: https://leetcode.com/problems/max-area-of-island/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0]) if m else 0
        dy = [0, -1, 0, 1]
        dx = [1, 0, -1, 0]
        res = 0

        def bfs(y, x):
            grid[y][x] = 0
            q = [[y,x]]
            area = 1
            while q:
                v = q.pop(0)
                for i in range(4):
                    y1 = v[0] + dy[i]
                    x1 = v[1] + dx[i]
                    if y1 < 0 or y1 >= m or x1 < 0 or x1 >= n or grid[y1][x1] == 0:
                        continue
                    grid[y1][x1] = 0
                    q.append([y1,x1])
                    area += 1
            return area

        for y in range(m):
            for x in range(n):
                if grid[y][x] == 0: continue
                res = max(res, bfs(y, x))

        return res

```
