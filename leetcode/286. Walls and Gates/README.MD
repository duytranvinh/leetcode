# [286. Walls and Gates (Medium)](https://leetcode.com/problems/walls-and-gates/)

<p>You are given an <code>m x n</code> grid <code>rooms</code>&nbsp;initialized with these three possible values.</p>

<ul>
	<li><code>-1</code>&nbsp;A wall or an obstacle.</li>
	<li><code>0</code> A gate.</li>
	<li><code>INF</code> Infinity means an empty room. We use the value <code>2<sup>31</sup> - 1 = 2147483647</code> to represent <code>INF</code> as you may assume that the distance to a gate is less than <code>2147483647</code>.</li>
</ul>

<p>Fill each empty room with the distance to <em>its nearest gate</em>. If it is impossible to reach a gate, it should be filled with <code>INF</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/03/grid.jpg" style="width: 500px; height: 223px;">
<pre><strong>Input:</strong> rooms = [[2147483647,-1,0,2147483647],[2147483647,2147483647,2147483647,-1],[2147483647,-1,2147483647,-1],[0,-1,2147483647,2147483647]]
<strong>Output:</strong> [[3,-1,0,1],[2,2,1,-1],[1,-1,2,-1],[0,-1,3,4]]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> rooms = [[-1]]
<strong>Output:</strong> [[-1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == rooms.length</code></li>
	<li><code>n == rooms[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 250</code></li>
	<li><code>rooms[i][j]</code> is <code>-1</code>, <code>0</code>, or <code>2<sup>31</sup> - 1</code>.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [DoorDash](https://leetcode.com/company/doordash), [Google](https://leetcode.com/company/google), [tiktok](https://leetcode.com/company/tiktok), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Spotify](https://leetcode.com/company/spotify)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Surrounded Regions (Medium)](https://leetcode.com/problems/surrounded-regions/)
- [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)
- [Shortest Distance from All Buildings (Hard)](https://leetcode.com/problems/shortest-distance-from-all-buildings/)
- [Robot Room Cleaner (Hard)](https://leetcode.com/problems/robot-room-cleaner/)
- [Rotting Oranges (Medium)](https://leetcode.com/problems/rotting-oranges/)

## Solution 1.

At first, we find our starting point which is all the Gates

From there, we do BFS for each valid cells

If `rooms[dy][dx] <= rooms[y][x] + 1`, which mean that `[dy, dx]` cell is already have a shorter path or a wall (Gate = 0, Wall = -1)

```py
# OJ: https://leetcode.com/problems/walls-and-gates/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        ROW, COL = len(rooms), len(rooms[0])
        dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        q = collections.deque()

        for y in range(ROW):
            for x in range(COL):
                if rooms[y][x] != 0: continue
                q.append((y, x))

        while q:
            cur = len(q)
            for _ in range(cur):
                y, x = q.popleft()
                for y1, x1 in dirs:
                    dy, dx = y + y1, x + x1
                    if dy < 0 or dy >= ROW or dx < 0 or dx >= COL:  continue
                    if rooms[dy][dx] <= rooms[y][x] + 1:            continue
                    rooms[dy][dx] = rooms[y][x] + 1
                    q.append((dy, dx))

```
