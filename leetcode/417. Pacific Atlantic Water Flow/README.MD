# [417. Pacific Atlantic Water Flow (Medium)](https://leetcode.com/problems/pacific-atlantic-water-flow/)

<p>There is an <code>m x n</code> rectangular island that borders both the <strong>Pacific Ocean</strong> and <strong>Atlantic Ocean</strong>. The <strong>Pacific Ocean</strong> touches the island's left and top edges, and the <strong>Atlantic Ocean</strong> touches the island's right and bottom edges.</p>

<p>The island is partitioned into a grid of square cells. You are given an <code>m x n</code> integer matrix <code>heights</code> where <code>heights[r][c]</code> represents the <strong>height above sea level</strong> of the cell at coordinate <code>(r, c)</code>.</p>

<p>The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is <strong>less than or equal to</strong> the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.</p>

<p>Return <em>a <strong>2D list</strong> of grid coordinates </em><code>result</code><em> where </em><code>result[i] = [r<sub>i</sub>, c<sub>i</sub>]</code><em> denotes that rain water can flow from cell </em><code>(r<sub>i</sub>, c<sub>i</sub>)</code><em> to <strong>both</strong> the Pacific and Atlantic oceans</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/06/08/waterflow-grid.jpg" style="width: 573px; height: 573px;">
<pre><strong>Input:</strong> heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
<strong>Output:</strong> [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> heights = [[2,1],[1,2]]
<strong>Output:</strong> [[0,0],[0,1],[1,0],[1,1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == heights.length</code></li>
	<li><code>n == heights[r].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= heights[r][c] &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber), [Salesforce](https://leetcode.com/company/salesforce)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

## Solution 1. DFS

For each cell, we search (go all four direction) until it's invalid

Invalid conditions are:

```
if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue
if (dy, dx) in visited:                         continue
if heights[dy][dx] < heights[y][x]:             continue
```

Instead of DFS through each cell in the array

We go backward from the sides/oceans

- Go through every cell in first and last row

- Go through every cell in first and last col

Use `set()` to keep track of visited cells, so we don't have to revisit the cell

This set is also used to keep track the number of cells that oceans can reach

```py
# OJ: https://leetcode.com/problems/pacific-atlantic-water-flow/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        ROW, COL = len(heights), len(heights[0])
        pac, atl = set(), set()
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        def dfs(y, x, visited, prevHeight):
            # if (y, x) in visited: return
            visited.add((y, x))
            for y1, x1 in dirs:
                dy, dx = y + y1, x + x1
                if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue
                if (dy, dx) in visited:                         continue
                if heights[dy][dx] < heights[y][x]:             continue
                dfs(dy, dx, visited, heights[y][x])

        #Go through every cel in first and last row
        for x in range(COL):
            dfs(0, x, pac, heights[0][x])
            dfs(ROW - 1, x, atl, heights[ROW - 1][x])

        #Go through every cel in first and last col
        for y in range(ROW):
            dfs(y, 0, pac, heights[y][0])
            dfs(y, COL - 1, atl, heights[y][COL - 1])

        res = list()
        for r in range(ROW):
            for c in range(COL):
                if (r, c) in pac and (r, c) in atl:
                    res.append([r, c])

        return res

```

## Solution 1. BFS

Same idea as DFS, but this time, we use BFS

We have two different queue for each oceans.

Starting with:

- Go through every cell in first and last row

- Go through every cell in first and last col

From that, we search (go all four direction) until it's invalid

At the end of BFS, we return `visited` set

```py
# OJ: https://leetcode.com/problems/pacific-atlantic-water-flow/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        ROW, COL = len(heights), len(heights[0])
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        def bfs(q):
            visited = set()
            while q:
                (y, x) = q.popleft()
                visited.add((y, x))
                for y1, x1 in dirs:
                    dy, dx = y + y1, x + x1
                    if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue
                    if (dy, dx) in visited:                         continue
                    if heights[dy][dx] < heights[y][x]:             continue
                    q.append((dy, dx))
            return visited

        # Setup a queue for the oceans
        pac, atl = collections.deque(), collections.deque()

        #Go through every cel in first and last row
        for x in range(COL):
            pac.append((0, x))
            atl.append((ROW - 1, x))

        #Go through every cel in first and last col
        for y in range(ROW):
            pac.append((y, 0))
            atl.append((y, COL - 1))

        pacificVisited = bfs(pac)
        atlanticVisited = bfs(atl)

        res = list()
        for y, x in pacificVisited:
            if (y, x) in atlanticVisited:
                res.append([y, x])

        return res
```
