# [547. Number of Provinces (Medium)](https://leetcode.com/problems/number-of-provinces)

<p>There are <code>n</code> cities. Some of them are connected, while some are not. If city <code>a</code> is connected directly with city <code>b</code>, and city <code>b</code> is connected directly with city <code>c</code>, then city <code>a</code> is connected indirectly with city <code>c</code>.</p>

<p>A <strong>province</strong> is a group of directly or indirectly connected cities and no other cities outside of the group.</p>

<p>You are given an <code>n x n</code> matrix <code>isConnected</code> where <code>isConnected[i][j] = 1</code> if the <code>i<sup>th</sup></code> city and the <code>j<sup>th</sup></code> city are directly connected, and <code>isConnected[i][j] = 0</code> otherwise.</p>

<p>Return <em>the total number of <strong>provinces</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg" style="width: 222px; height: 142px;" />
<pre>
<strong>Input:</strong> isConnected = [[1,1,0],[1,1,0],[0,0,1]]
<strong>Output:</strong> 2
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg" style="width: 222px; height: 142px;" />
<pre>
<strong>Input:</strong> isConnected = [[1,0,0],[0,1,0],[0,0,1]]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 200</code></li>
	<li><code>n == isConnected.length</code></li>
	<li><code>n == isConnected[i].length</code></li>
	<li><code>isConnected[i][j]</code> is <code>1</code> or <code>0</code>.</li>
	<li><code>isConnected[i][i] == 1</code></li>
	<li><code>isConnected[i][j] == isConnected[j][i]</code></li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Sprinklr](https://leetcode.com/company/sprinklr), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [TikTok](https://leetcode.com/company/tiktok), [Two Sigma](https://leetcode.com/company/two-sigma)

**Related Topics**:  
[Depth-First Search](https://leetcode.com/tag/depth-first-search), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search), [Union Find](https://leetcode.com/tag/union-find), [Graph](https://leetcode.com/tag/graph)

**Similar Questions**:

- [Number of Connected Components in an Undirected Graph (Medium)](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph)
- [Robot Return to Origin (Easy)](https://leetcode.com/problems/robot-return-to-origin)
- [Sentence Similarity (Easy)](https://leetcode.com/problems/sentence-similarity)
- [Sentence Similarity II (Medium)](https://leetcode.com/problems/sentence-similarity-ii)
- [The Earliest Moment When Everyone Become Friends (Medium)](https://leetcode.com/problems/the-earliest-moment-when-everyone-become-friends)
- [Detonate the Maximum Bombs (Medium)](https://leetcode.com/problems/detonate-the-maximum-bombs)

## Solution 1. BFS with adj list

```py
# OJ: https://leetcode.com/problems/number-of-provinces
# Author: Duy Tran
# Time: O(N^2)
# Space: O(N^2)

class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        n = len(isConnected)
        edges = [[] for _ in range(n)]
        for i in range(n):
            for j in range(n):
                if i == j: continue
                if isConnected[i][j] == 1:
                    edges[i].append(j)
                    edges[j].append(i)
        visited = [0 for _ in range(n)]
        count = 0
        for i in range(n):
            if (visited[i] == 1): continue
            visited[i] = 1
            count += 1
            q = []
            q.append(i)
            while (len(q)):
                u = q.pop(0)
                cur = len(edges[u])
                for j in range(cur):
                    v = edges[u][j]
                    if (visited[v] == 1): continue
                    visited[v] = 1
                    q.append(v)

        return count

```
