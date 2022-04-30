# [694. Number of Distinct Islands (Medium)](https://leetcode.com/problems/number-of-distinct-islands/)

<p>You are given an <code>m x n</code> binary matrix <code>grid</code>. An island is a group of <code>1</code>'s (representing land) connected <strong>4-directionally</strong> (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.</p>

<p>An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.</p>

<p>Return <em>the number of <b>distinct</b> islands</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/01/distinctisland1-1-grid.jpg" style="width: 413px; height: 334px;">
<pre><strong>Input:</strong> grid = [[1,1,0,0,0],[1,1,0,0,0],[0,0,0,1,1],[0,0,0,1,1]]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/01/distinctisland1-2-grid.jpg" style="width: 413px; height: 334px;">
<pre><strong>Input:</strong> grid = [[1,1,0,1,1],[1,0,0,0,0],[0,0,0,0,1],[1,1,0,1,1]]
<strong>Output:</strong> 3
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
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Hash Function](https://leetcode.com/tag/hash-function/)

**Similar Questions**:

- [Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)
- [Number of Distinct Islands II (Hard)](https://leetcode.com/problems/number-of-distinct-islands-ii/)
- [Count Sub Islands (Medium)](https://leetcode.com/problems/count-sub-islands/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/number-of-distinct-islands/
# Author: Duy Tran
# Time: O(M * N)
# Space: O(M * N) for the Queue

class Solution:
    #BFS
    #Map (calculate the distance) the path into set
    #set is unique val
    #any same path will be count as 1
    def numDistinctIslands(self, grid: List[List[int]]) -> int:
        s = set()
        m = len(grid)
        n = len(grid[0]) if m else 0
        dy = [0, -1, 0, 1]
        dx = [1, 0, -1, 0]
        for y in range(m):
            for x in range(n):
                if grid[y][x] == 0: continue
                grid[y][x] = 0
                path = str()
                q = [[y,x]]
                while q:
                    v = q.pop(0)
                    for i in range(4):
                        y1 = v[0] + dy[i]
                        x1 = v[1] + dx[i]
                        if y1 < 0 or y1 >= m or x1 < 0 or x1 >= n or grid[y1][x1] == 0:
                            continue
                        q.append([y1,x1])
                        grid[y1][x1] = 0
                        path += str(y1 - y) + str(x1 - x)
                s.add(path)
        return len(s)
```
