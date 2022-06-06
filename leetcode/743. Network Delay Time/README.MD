# [743. Network Delay Time (Medium)](https://leetcode.com/problems/network-delay-time/)

<p>You are given a network of <code>n</code> nodes, labeled from <code>1</code> to <code>n</code>. You are also given <code>times</code>, a list of travel times as directed edges <code>times[i] = (u<sub>i</sub>, v<sub>i</sub>, w<sub>i</sub>)</code>, where <code>u<sub>i</sub></code> is the source node, <code>v<sub>i</sub></code> is the target node, and <code>w<sub>i</sub></code> is the time it takes for a signal to travel from source to target.</p>

<p>We will send a signal from a given node <code>k</code>. Return <em>the <strong>minimum</strong> time it takes for all the</em> <code>n</code> <em>nodes to receive the signal</em>. If it is impossible for all the <code>n</code> nodes to receive the signal, return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png" style="width: 217px; height: 239px;">
<pre><strong>Input:</strong> times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
<strong>Output:</strong> 2
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> times = [[1,2,1]], n = 2, k = 1
<strong>Output:</strong> 1
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> times = [[1,2,1]], n = 2, k = 2
<strong>Output:</strong> -1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= n &lt;= 100</code></li>
	<li><code>1 &lt;= times.length &lt;= 6000</code></li>
	<li><code>times[i].length == 3</code></li>
	<li><code>1 &lt;= u<sub>i</sub>, v<sub>i</sub> &lt;= n</code></li>
	<li><code>u<sub>i</sub> != v<sub>i</sub></code></li>
	<li><code>0 &lt;= w<sub>i</sub> &lt;= 100</code></li>
	<li>All the pairs <code>(u<sub>i</sub>, v<sub>i</sub>)</code> are <strong>unique</strong>. (i.e., no multiple edges.)</li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Shortest Path](https://leetcode.com/tag/shortest-path/)

**Similar Questions**:

- [The Time When the Network Becomes Idle (Medium)](https://leetcode.com/problems/the-time-when-the-network-becomes-idle/)
- [Second Minimum Time to Reach Destination (Hard)](https://leetcode.com/problems/second-minimum-time-to-reach-destination/)

## Solution 1. Dijkstra

1. Build up `edges` hashmap with `key = u` and `value` is the array that `u` connect to and its weight `[(weight, v)]`

2. We use `minHeap` to keep track the smallest weight and its destination. We keep `(w, v)` with `v` is from `k` to `v`

3. We loop through our `queue` and until all `node` is `visited`

   - This work because we use `minHeap`, so only the smallest path is popped

   1. We pop the minimum number in `minHeap`

   2. Add it into our `visited`

   3. Loop through our `edges`

   4. If `v` is not `visited`, add it into our `minHeap`

4. Return `res` if all nodes is `visited`

```py
# OJ: https://leetcode.com/problems/network-delay-time/
# Author: Duy Tran
# Time: O(E + E * logV)
# Space: O(E)

class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        edges = collections.defaultdict(list)
        for u, v, w in times:
            edges[u].append((w, v))

        minHeap = [(0, k)]
        visited = set()
        res = 0

        while minHeap and len(visited) < n:
            wU, u = heapq.heappop(minHeap)
            visited.add(u)
            res = max(res, wU)

            for wUV, v in edges[u]:
                if v in visited: continue
                heapq.heappush(minHeap, (wU + wUV, v))

        return res if len(visited) == n else -1
```

## Solution 2. Bellman Ford

This solution is not sufficient because we travel all the edges N times

But here's it

1. We build up `dist` array. `dist[i]` is the the weight from `k` to `i`

2. With every node from `1` to `n`, we loop through all the `edges`

3. We update the `dist` array by finding the minimum `dist[v]` and `dist[u] + wUV`

4. After we done, we check through our array again. If one node is not visited, we return `-1`. Else return the maximum

```py
# OJ: https://leetcode.com/problems/network-delay-time/
# Author: Duy Tran
# Time: O(VE)
# Space: O(V)

class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        dist = [float("inf") for _ in range(n + 1)]
        dist[k] = 0

        for i in range(1, n + 1):
            for u, v, w in times:
                if dist[u] == float("inf"): continue
                dist[v] = min(dist[v], dist[u] + w)

        res = 0
        for i in range(1, n + 1):
            if dist[i] == float("inf"): return -1
            res = max(res, dist[i])

        return res

```
