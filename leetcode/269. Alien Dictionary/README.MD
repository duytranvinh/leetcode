# [269. Alien Dictionary (Hard)](https://leetcode.com/problems/alien-dictionary/)

<p>There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.</p>

<p>You are given a list of strings <code>words</code> from the alien language's dictionary, where the strings in <code>words</code> are <strong>sorted lexicographically</strong> by the rules of this new language.</p>

<p>Return <em>a string of the unique letters in the new alien language sorted in <strong>lexicographically increasing order</strong> by the new language's rules. If there is no solution, return </em><code>""</code><em>. If there are multiple solutions, return <strong>any of them</strong></em>.</p>

<p>A string <code>s</code> is <strong>lexicographically smaller</strong> than a string <code>t</code> if at the first letter where they differ, the letter in <code>s</code> comes before the letter in <code>t</code> in the alien language. If the first <code>min(s.length, t.length)</code> letters are the same, then <code>s</code> is smaller if and only if <code>s.length &lt; t.length</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["wrt","wrf","er","ett","rftt"]
<strong>Output:</strong> "wertf"
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["z","x"]
<strong>Output:</strong> "zx"
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> words = ["z","x","z"]
<strong>Output:</strong> ""
<strong>Explanation:</strong> The order is invalid, so return <code>""</code>.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 100</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 100</code></li>
	<li><code>words[i]</code> consists of only lowercase English letters.</li>
</ul>

**Companies**:  
[Airbnb](https://leetcode.com/company/airbnb), [Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [Snapchat](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/), [Graph](https://leetcode.com/tag/graph/), [Topological Sort](https://leetcode.com/tag/topological-sort/)

**Similar Questions**:

- [Course Schedule II (Medium)](https://leetcode.com/problems/course-schedule-ii/)

## Solution 1. Topological Sort (DFS)

Post-order DFS

1. Build adjacency list `adj`

   - Initial the hashmap with `key = c` and `value = set()`

     - Double for loop: for `w` in `words` -> for `c` in `w`

     - `adj[c] = set()`

   - Update our hashmap

     - Take two words `w1 = words[i]` and `w2 = words[i + 1]`

     - We take `minLen` of two words. Why minLength? Because we will loop through two words

     - Invalid case: if length `w1` > `w2` and have the same prefix `w[:minLen]`: return `""`

       - Why this is invalid?

       - In dictionary, `i <= i + 1`, if we have same prefix, length of `w1` can't be longer than `w2`

       - `abc` vs `ab` is invalid order, need to be `ab` vs `abc`

     - Loop through every `c` in `w1` and `w2`

       - If `w1[c] != w2[c]`, then we add that `c` into our `adj[w1[c]].add(w2[c])`

2. Loop through every `c` in `adj`, do the DFS if it's not `visited`

   - DFS(`c`)

   - We mark `visited[c] = True` to say that we currently visiting this `c` in the path

   - Then we loop throuhg it `nei` in `adj[c]`

     - If it is not `visited`, then we do `dfs(nei)`

     - If it is CURRENTLY `visited` in our path, return `True` which means a cycle detected

   - We mark `visited[c] = False` to say that this `c` is visted but we currently NOT visiting this `c` in the path anymore

   - Add `c` into our `res`

3. If we have a cycle, return `""`

4. Reverse our `res`

   - Since we add our `c` in at the end of our path.

   - So the `res` will have reversed order

5. Return `res` as a string

```py
# OJ: https://leetcode.com/problems/alien-dictionary/
# Author: Duy Tran
# Time: O(N)
# Space: O(1) or O(26) max

class Solution:
    def alienOrder(self, words: List[str]) -> str:
        adj = { c: set() for w in words for c in w }
        n = len(words)

        for i in range(n - 1):
            w1, w2 = words[i], words[i + 1]
            minLen = min(len(w1), len(w2))
            if len(w1) > len(w2) and w1[:minLen] == w2[:minLen]:
                return ""
            for j in range(minLen):
                if w1[j] != w2[j]:
                    adj[w1[j]].add(w2[j])
                    break

        visited = dict()
        res = list()

        def dfs(c):
            # if c in visited:
            #     return visited[c]
            visited[c] = True
            for nei in adj[c]:
                if nei not in visited and dfs(nei):
                    return True
                if visited[nei] == True:
                    return True
            visited[c] = False
            res.append(c)

        for c in adj:
            if c not in visited and dfs(c):
                return ""

        res.reverse()
        return "".join(res)

```

## Solution 1. Topological Sort (BFS)

1. Build adjacency list `adj`

2. Build `indegree` hashmap with `indegree[v] = number of u connect to v`

3. If `indegree[v] == 0`, add it to our `queue`

4. Then do BFS

    - We pop `u` from our `queue`

    - Loop though it neighbors in `adj[u]`

    - Mark that `uv` connection is visited by `indegree[v]--`

    - Only `v` that have `indegree[v] == 0` will be added to `q.append(v)`

5. Return `res` if length `res == adj` where all `c` has been visited

```py
# OJ: https://leetcode.com/problems/alien-dictionary/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def alienOrder(self, words: List[str]) -> str:
        adj = { c: set() for w in words for c in w }
        n = len(words)

        for i in range(n - 1):
            w1, w2 = words[i], words[i + 1]
            minLen = min(len(w1), len(w2))
            if len(w1) > len(w2) and w1[:minLen] == w2[:minLen]:
                return ""
            for j in range(minLen):
                if w1[j] != w2[j]:
                    adj[w1[j]].add(w2[j])
                    break

        indegree = {c: 0 for c in adj}
        for u, neighbors in adj.items():
            for v in neighbors:
                indegree[v] += 1

        q = collections.deque()
        for v, count in indegree.items():
            if count == 0: q.append(v)

        res = list()
        while q:
            u = q.popleft()
            res.append(u)
            for v in adj[u]:
                indegree[v] -= 1
                if indegree[v] == 0:
                    q.append(v)

        return "".join(res) if len(res) == len(adj) else ""
```
