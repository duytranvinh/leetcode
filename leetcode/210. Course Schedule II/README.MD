# [210. Course Schedule II (Medium)](https://leetcode.com/problems/course-schedule-ii/)

<p>There are a total of <code>numCourses</code> courses you have to take, labeled from <code>0</code> to <code>numCourses - 1</code>. You are given an array <code>prerequisites</code> where <code>prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>]</code> indicates that you <strong>must</strong> take course <code>b<sub>i</sub></code> first if you want to take course <code>a<sub>i</sub></code>.</p>

<ul>
	<li>For example, the pair <code>[0, 1]</code>, indicates that to take course <code>0</code> you have to first take course <code>1</code>.</li>
</ul>

<p>Return <em>the ordering of courses you should take to finish all courses</em>. If there are many valid answers, return <strong>any</strong> of them. If it is impossible to finish all courses, return <strong>an empty array</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> numCourses = 2, prerequisites = [[1,0]]
<strong>Output:</strong> [0,1]
<strong>Explanation:</strong> There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
<strong>Output:</strong> [0,2,1,3]
<strong>Explanation:</strong> There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> numCourses = 1, prerequisites = []
<strong>Output:</strong> [0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numCourses &lt;= 2000</code></li>
	<li><code>0 &lt;= prerequisites.length &lt;= numCourses * (numCourses - 1)</code></li>
	<li><code>prerequisites[i].length == 2</code></li>
	<li><code>0 &lt;= a<sub>i</sub>, b<sub>i</sub> &lt; numCourses</code></li>
	<li><code>a<sub>i</sub> != b<sub>i</sub></code></li>
	<li>All the pairs <code>[a<sub>i</sub>, b<sub>i</sub>]</code> are <strong>distinct</strong>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Robinhood](https://leetcode.com/company/robinhood), [Roblox](https://leetcode.com/company/roblox), [Karat](https://leetcode.com/company/karat), [Twilio](https://leetcode.com/company/twilio), [VMware](https://leetcode.com/company/vmware), [Facebook](https://leetcode.com/company/facebook), [Salesforce](https://leetcode.com/company/salesforce), [ByteDance](https://leetcode.com/company/bytedance), [Wayfair](https://leetcode.com/company/wayfair)

**Related Topics**:  
[Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Topological Sort](https://leetcode.com/tag/topological-sort/)

**Similar Questions**:

- [Course Schedule (Medium)](https://leetcode.com/problems/course-schedule/)
- [Alien Dictionary (Hard)](https://leetcode.com/problems/alien-dictionary/)
- [Minimum Height Trees (Medium)](https://leetcode.com/problems/minimum-height-trees/)
- [Sequence Reconstruction (Medium)](https://leetcode.com/problems/sequence-reconstruction/)
- [Course Schedule III (Hard)](https://leetcode.com/problems/course-schedule-iii/)
- [Parallel Courses (Medium)](https://leetcode.com/problems/parallel-courses/)
- [Find All Possible Recipes from Given Supplies (Medium)](https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies/)

## Solution 1. Topological Sort

Refer to [207. Course Schedule](/leetcode/207.%20Course%20Schedule/)

We build up the `edges` array `edges[u] = [v]` where `u = pre` and `v = courses`

We also build the `indegree` array to keep track number of `pre` that point into `course`

We only add `u` into our `q` if and only if `indegree[u] == 0`. Which mean all the prerequisite has been "captured"

For every `u`, when we do BFS in all `v` in `edges[u]`.

We gonna do `indegree[v] -= 1`

In the good scenario, no cycle, all `indegree[v]` will be `0` at the end.

Since we only add `v` to `q` `indegree[v] == 0`, whenever there's a cycle, the `indegree[v]` will NEVER be `0`

```py

# OJ: https://leetcode.com/problems/course-schedule-ii/
# Author: Duy Tran
# Time: O(N + E), N is the number of courses, E is the number of edges
# Space: O(N + E)

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
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

        res = list()
        while q:
            u = q.popleft()
            for v in edges[u]:
                indegree[v] -= 1
                if indegree[v] == 0:
                    q.append(v)
            res.append(u)

        for course in range(numCourses):
            if indegree[course] != 0:
                return []
        return res

```
