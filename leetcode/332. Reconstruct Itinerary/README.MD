# [332. Reconstruct Itinerary (Hard)](https://leetcode.com/problems/reconstruct-itinerary/)

<p>You are given a list of airline <code>tickets</code> where <code>tickets[i] = [from<sub>i</sub>, to<sub>i</sub>]</code> represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.</p>

<p>All of the tickets belong to a man who departs from <code>"JFK"</code>, thus, the itinerary must begin with <code>"JFK"</code>. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.</p>

<ul>
	<li>For example, the itinerary <code>["JFK", "LGA"]</code> has a smaller lexical order than <code>["JFK", "LGB"]</code>.</li>
</ul>

<p>You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/14/itinerary1-graph.jpg" style="width: 382px; height: 222px;">
<pre><strong>Input:</strong> tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
<strong>Output:</strong> ["JFK","MUC","LHR","SFO","SJC"]
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/14/itinerary2-graph.jpg" style="width: 222px; height: 230px;">
<pre><strong>Input:</strong> tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
<strong>Output:</strong> ["JFK","ATL","JFK","SFO","ATL","SFO"]
<strong>Explanation:</strong> Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"] but it is larger in lexical order.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= tickets.length &lt;= 300</code></li>
	<li><code>tickets[i].length == 2</code></li>
	<li><code>from<sub>i</sub>.length == 3</code></li>
	<li><code>to<sub>i</sub>.length == 3</code></li>
	<li><code>from<sub>i</sub></code> and <code>to<sub>i</sub></code> consist of uppercase English letters.</li>
	<li><code>from<sub>i</sub> != to<sub>i</sub></code></li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Facebook](https://leetcode.com/company/facebook), [Twitter](https://leetcode.com/company/twitter), [Netflix](https://leetcode.com/company/netflix)

**Related Topics**:  
[Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Eulerian Circuit](https://leetcode.com/tag/eulerian-circuit/)

**Similar Questions**:

- [Longest Common Subpath (Hard)](https://leetcode.com/problems/longest-common-subpath/)
- [Valid Arrangement of Pairs (Hard)](https://leetcode.com/problems/valid-arrangement-of-pairs/)

## Solution 1. DFS

1. We build our adjacency list `edges`

2. Since we start at `JFK`, we add `JFK` to our `res` and start `dfs(JFK)`

3. DFS

   - We loop through `edges[u]`. Since some language don't allow to mutate data and looping it at the same time, we use a placeholder `neighbors`

     - We temporary remove `v` out of our `edges[u]`

     - We temporary add `v` into our `res`

       - If by add `v` into `res`, make our path completed `len(res) == len(tickets) + 1`, we return `True`

       - If `v` not in our adjacency list `edges`, that means that path is a dead-end, no need to go into that path

       - If `v` in our adjacency list `edges`, we do `dfs(v)`

       - We that path `True`, return `True` and stop our loop iteration

       - We add `v` back in our `edges[u]`

       - We remove `v` out of our `res`

   - If we somehow cannot find a path, we return `False`. But it's not necessarily since THIS LEETCODE guaranteed we have a paths (ask interviewer about it)

```py

# OJ: https://leetcode.com/problems/reconstruct-itinerary/
# Author: Duy Tran
# Time: O(E^2)
# Space: O(E)

class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        tickets.sort()
        edges = { src: [] for src, dst in tickets}

        for src, dst in tickets:
            edges[src].append(dst)

        res = list()
        res.append("JFK")

        def dfs(u):
            neighbors = edges[u]
            for i, v in enumerate(neighbors):
                edges[u].pop(i)
                res.append(v)

                if len(res) == len(tickets) + 1:    return True
                if v in edges and dfs(v):           return True

                edges[u].insert(i, v)
                res.pop()

            # return False

        dfs("JFK")
        return res

```
