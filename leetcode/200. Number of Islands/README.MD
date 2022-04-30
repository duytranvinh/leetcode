# [200. Number of Islands (Medium)](https://leetcode.com/problems/number-of-islands/)

<p>Given an <code>m x n</code> 2D binary grid <code>grid</code> which represents a map of <code>'1'</code>s (land) and <code>'0'</code>s (water), return <em>the number of islands</em>.</p>

<p>An <strong>island</strong> is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
<strong>Output:</strong> 1
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 300</code></li>
	<li><code>grid[i][j]</code> is <code>'0'</code> or <code>'1'</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Facebook](https://leetcode.com/company/facebook), [Google](https://leetcode.com/company/google), [LinkedIn](https://leetcode.com/company/linkedin), [Oracle](https://leetcode.com/company/oracle), [Apple](https://leetcode.com/company/apple), [Salesforce](https://leetcode.com/company/salesforce), [tiktok](https://leetcode.com/company/tiktok), [Uber](https://leetcode.com/company/uber), [SAP](https://leetcode.com/company/sap), [ByteDance](https://leetcode.com/company/bytedance), [Docusign](https://leetcode.com/company/docusign), [ServiceNow](https://leetcode.com/company/servicenow), [Shopee](https://leetcode.com/company/shopee), [Qualtrics](https://leetcode.com/company/qualtrics), [Dropbox](https://leetcode.com/company/dropbox), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Nvidia](https://leetcode.com/company/nvidia)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Union Find](https://leetcode.com/tag/union-find/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Surrounded Regions (Medium)](https://leetcode.com/problems/surrounded-regions/)
- [Walls and Gates (Medium)](https://leetcode.com/problems/walls-and-gates/)
- [Number of Islands II (Hard)](https://leetcode.com/problems/number-of-islands-ii/)
- [Number of Connected Components in an Undirected Graph (Medium)](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)
- [Number of Distinct Islands (Medium)](https://leetcode.com/problems/number-of-distinct-islands/)
- [Max Area of Island (Medium)](https://leetcode.com/problems/max-area-of-island/)
- [Count Sub Islands (Medium)](https://leetcode.com/problems/count-sub-islands/)
- [Find All Groups of Farmland (Medium)](https://leetcode.com/problems/find-all-groups-of-farmland/)

## Solution 1. BFS

```py
# OJ: https://leetcode.com/problems/number-of-islands/
# Author: Duy Tran
# Time: O(M * N)
# Space: O(M * N), the Queue could be full

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid)
        n = len(grid[0]) if m else 0
        count = 0
        dy = [-1, 0, 1, 0]
        dx = [0, 1, 0, -1]
        for y in range(m):
            for x in range(n):
                if grid[y][x] == '0': continue
                grid[y][x] = '0'
                count += 1
                q = list()
                q.append([y,x])
                while q:
                    v = q[0]
                    q.pop(0)
                    for i in range(4):
                        y1 = v[0] + dy[i]
                        x1 = v[1] + dx[i]
                        if y1 < 0 or y1 >= m or x1 < 0 or x1 >= n:
                            continue
                        if grid[y1][x1] == '0': continue
                        q.append([y1,x1])
                        grid[y1][x1] = '0'
        return count
```
