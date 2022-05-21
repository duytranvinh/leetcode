# [815. Bus Routes (Hard)](https://leetcode.com/problems/bus-routes/)

<p>You are given an array <code>routes</code> representing bus routes where <code>routes[i]</code> is a bus route that the <code>i<sup>th</sup></code> bus repeats forever.</p>

<ul>
	<li>For example, if <code>routes[0] = [1, 5, 7]</code>, this means that the <code>0<sup>th</sup></code> bus travels in the sequence <code>1 -&gt; 5 -&gt; 7 -&gt; 1 -&gt; 5 -&gt; 7 -&gt; 1 -&gt; ...</code> forever.</li>
</ul>

<p>You will start at the bus stop <code>source</code> (You are not on any bus initially), and you want to go to the bus stop <code>target</code>. You can travel between bus stops by buses only.</p>

<p>Return <em>the least number of buses you must take to travel from </em><code>source</code><em> to </em><code>target</code>. Return <code>-1</code> if it is not possible.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> routes = [[1,2,7],[3,6,7]], source = 1, target = 6
<strong>Output:</strong> 2
<strong>Explanation:</strong> The best strategy is take the first bus to the bus stop 7, then take the second bus to the bus stop 6.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> routes = [[7,12],[4,5,15],[6],[15,19],[9,12,13]], source = 15, target = 12
<strong>Output:</strong> -1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= routes.length &lt;= 500</code>.</li>
	<li><code>1 &lt;= routes[i].length &lt;= 10<sup>5</sup></code></li>
	<li>All the values of <code>routes[i]</code> are <strong>unique</strong>.</li>
	<li><code>sum(routes[i].length) &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= routes[i][j] &lt; 10<sup>6</sup></code></li>
	<li><code>0 &lt;= source, target &lt; 10<sup>6</sup></code></li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/)

## Solution 1. BFS

Shortest path => BFS

We build up the `edges` map with `key = station` and `value = [buses]`. Which `bus` will be visit that `station`

We don't want to visit the same `station` or `bus` during our BFS

```py
# OJ: https://leetcode.com/problems/bus-routes/
# Author: Duy Tran
# Time: O(N) where N is the sum of lengths of elements in `routes`
# Space: O(N)

class Solution:
    def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
        n = len(routes)
        step = 0
        stations = defaultdict(list)
        for i, route in enumerate(routes):
            for num in route:
                stations[num].append(i)
        visitedStation = set([source])
        visitedBus = set()
        q = [source]
        while q:
            cnt = len(q)
            for _ in range(cnt):
                u = q.pop(0)
                if u == target: return step
                for bus in stations[u]:
                    if bus in visitedBus: continue
                    visitedBus.add(bus)
                    for station in routes[bus]:
                        if station in visitedStation: continue
                        q.append(station)
                        visitedStation.add(station)
            step += 1
        return -1

```
