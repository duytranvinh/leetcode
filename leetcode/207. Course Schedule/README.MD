# [207. Course Schedule (Medium)](https://leetcode.com/problems/course-schedule/)

<p>There are a total of <code>numCourses</code> courses you have to take, labeled from <code>0</code> to <code>numCourses - 1</code>. You are given an array <code>prerequisites</code> where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you <strong>must</strong> take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.</p>

<ul>
	<li>For example, the pair <code>[0, 1]</code>, indicates that to take course <code>0</code> you have to first take course <code>1</code>.</li>
</ul>

<p>Return <code>true</code> if you can finish all courses. Otherwise, return <code>false</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> numCourses = 2, prerequisites = [[1,0]]
<strong>Output:</strong> true
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> numCourses = 2, prerequisites = [[1,0],[0,1]]
<strong>Output:</strong> false
<strong>Explanation:</strong> There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numCourses &lt;= 2000</code></li>
	<li><code>0 &lt;= prerequisites.length &lt;= 5000</code></li>
	<li><code>prerequisites[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; numCourses</code></li>
	<li>All the pairs prerequisites[i] are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [tiktok](https://leetcode.com/company/tiktok), [Google](https://leetcode.com/company/google), [Uber](https://leetcode.com/company/uber), [Bloomberg](https://leetcode.com/company/bloomberg), [Oracle](https://leetcode.com/company/oracle), [Apple](https://leetcode.com/company/apple), [Salesforce](https://leetcode.com/company/salesforce), [ByteDance](https://leetcode.com/company/bytedance), [Qualtrics](https://leetcode.com/company/qualtrics), [Wayfair](https://leetcode.com/company/wayfair)

**Related Topics**:  
[Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Topological Sort](https://leetcode.com/tag/topological-sort/)

**Similar Questions**:

- [Course Schedule II (Medium)](https://leetcode.com/problems/course-schedule-ii/)
- [Graph Valid Tree (Medium)](https://leetcode.com/problems/graph-valid-tree/)
- [Minimum Height Trees (Medium)](https://leetcode.com/problems/minimum-height-trees/)
- [Course Schedule III (Hard)](https://leetcode.com/problems/course-schedule-iii/)

## Solution 1. DFS

We build up the `edges` array where `i = course` and `edges[i] = the array of prerequisites of i`

We use a set to keep track of the visited course

We do DFS starting at course `0`

When we do DFS

- If the `pre` is in `visited`, then we had saw that before, so there's a cycle in the graph => `False`

- After we done with that path, we remove it from `visited` and `edges[course] = []`

```py

# OJ: https://leetcode.com/problems/course-schedule/
# Author: Duy Tran
# Time: O(N + E), E is the edges
# Space: O(N + E)

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        edges = [ [] for _ in range(numCourses)]
        for course, pre in prerequisites:
            edges[course].append(pre)
        visited = set()

        def dfs(course):
            visited.add(course)
            for pre in edges[course]:
                if pre in visited:   return False
                if edges[pre] == []: continue
                if not dfs(pre):     return False
            visited.remove(course)
            edges[course] = []
            return True

        for course in range(numCourses):
            if not dfs(course): return False

        return True

```

## Solution 2. Topological Sort

We build up the `edges` array `edges[u] = [v]` where `u = pre` and `v = courses`

We also build the `indegree` array to keep track number of `pre` that point into `course`

We only add `u` into our `q` if and only if `indegree[u] == 0`. Which mean all the prerequisite has been "captured"

For every `u`, when we do BFS in all `v` in `edges[u]`.

We gonna do `indegree[v] -= 1`

In the good scenario, no cycle, all `indegree[v]` will be `0` at the end.

Since we only add `v` to `q` `indegree[v] == 0`, whenever there's a cycle, the `indegree[v]` will NEVER be `0`

```py
# OJ: https://leetcode.com/problems/course-schedule/
# Author: Duy Tran
# Time: O(N + E)
# Space: O(N)

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        edges = [ [] for _ in range(numCourses)]
        indegree = [ 0 for _ in range(numCourses)]
        for course, pre in prerequisites:
            edges[pre].append(course)
            indegree[course] += 1

        q = collections.deque()
        # looking for start point
        for i in range(numCourses):
            if indegree[i] != 0: continue
            q.append(i)

        while q:
            u = q.popleft()
            for v in edges[u]:
                indegree[v] -= 1
                if indegree[v] == 0:
                    q.append(v)

        for course in range(numCourses):
            if indegree[course] != 0:
                return False
        return True
```
