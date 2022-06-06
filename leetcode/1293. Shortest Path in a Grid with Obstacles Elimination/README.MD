# [1293. Shortest Path in a Grid with Obstacles Elimination (Hard)](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

<p>You are given an <code>m x n</code> integer matrix <code>grid</code> where each cell is either <code>0</code> (empty) or <code>1</code> (obstacle). You can move up, down, left, or right from and to an empty cell in <strong>one step</strong>.</p>

<p>Return <em>the minimum number of <strong>steps</strong> to walk from the upper left corner </em><code>(0, 0)</code><em> to the lower right corner </em><code>(m - 1, n - 1)</code><em> given that you can eliminate <strong>at most</strong> </em><code>k</code><em> obstacles</em>. If it is not possible to find such walk return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/09/30/short1-grid.jpg" style="width: 244px; height: 405px;">
<pre><strong>Input:</strong> grid = [[0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0]], k = 1
<strong>Output:</strong> 6
<strong>Explanation:</strong> 
The shortest path without eliminating any obstacle is 10.
The shortest path with one obstacle elimination at position (3,2) is 6. Such path is (0,0) -&gt; (0,1) -&gt; (0,2) -&gt; (1,2) -&gt; (2,2) -&gt; <strong>(3,2)</strong> -&gt; (4,2).
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/09/30/short2-grid.jpg" style="width: 244px; height: 245px;">
<pre><strong>Input:</strong> grid = [[0,1,1],[1,1,1],[1,0,0]], k = 1
<strong>Output:</strong> -1
<strong>Explanation:</strong> We need to eliminate at least two obstacles to find such a walk.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 40</code></li>
	<li><code>1 &lt;= k &lt;= m * n</code></li>
	<li><code>grid[i][j]</code> is either <code>0</code> <strong>or</strong> <code>1</code>.</li>
	<li><code>grid[0][0] == grid[m - 1][n - 1] == 0</code></li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Pinterest](https://leetcode.com/company/pinterest), [Microsoft](https://leetcode.com/company/microsoft), [Uber](https://leetcode.com/company/uber), [tiktok](https://leetcode.com/company/tiktok), [Snapchat](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Shortest Path to Get Food (Medium)](https://leetcode.com/problems/shortest-path-to-get-food/)
- [Minimum Obstacle Removal to Reach Corner (Hard)](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner/)

## Solution 1.

We can break down the algorithm into the following steps:

- BFS has a `queue`, and a set `visited` which keeps track of all the states visited along the way so that we don't visit the same state twice. `state = (y, x, k)`

- The element which popped from `queue` contains `steps` as well as the current state which `(y, x)` and the remaining `k`.

- We move all four directions. Each move results in a new state and the state is valid if it is within the grid boundaries and has not been visited before.

- Each valid state is pushed into the `queue`. Meanwhile, we also need to mark the `newState` as `visited`.

- At any iteration, if we have reached our `target`, we can return `steps` immediately.

**Note:** before running the BFS traversal, we also perform a quick check to see if we have sufficient `k` to take the most direct path from start to finish regardless of the number of obstacles. If so, the shortest distance to reach the target is the Manhattan distance between the starting cell and the target cell. Manhattan distance is `(ROW - 1) + (COL - 1) = ROW + COL - 2`

**Complexity**

We conduct a BFS traversal in the grid. In the worst case, we will visit each cell in the grid. And for each cell, at most, it will be visited `K` times, with different quotas of obstacle elimination.

Thus, the overall time complexity of the algorithm is `O(N⋅K)`

```py
# OJ: https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/
# Author: Duy Tran
# Time: O(N*K)
# Space: O(N*K)

class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        ROW, COL = len(grid), len(grid[0])
        # If k >= number of cells
        if k >= ROW + COL - 2:
            return ROW + COL - 2

        target = (ROW - 1, COL - 1)
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        state = (0, 0, k) #y, x, k

        q = collections.deque()
        visited = set()
        q.append((0, state))
        visited.add(set)

        while q:
            steps, (y, x, k) = q.popleft()

            if (y, x) == target:
                return steps

            for y1, x1 in dirs:
                dy, dx = y + y1, x + x1
                if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue

                dk = k - grid[y][x]
                newState = (dy, dx, dk)
                if dk < 0:              continue
                if newState in visited: continue

                q.append((steps + 1, newState))
                visited.add(newState)

        return -1
```
