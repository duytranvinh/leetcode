# [427. Construct Quad Tree (Medium)](https://leetcode.com/problems/construct-quad-tree/)

<p>Given a <code>n * n</code> matrix <code>grid</code> of <code>0's</code> and <code>1's</code> only. We want to represent the <code>grid</code> with a Quad-Tree.</p>

<p>Return <em>the root of the Quad-Tree</em> representing the <code>grid</code>.</p>

<p>Notice that you can assign the value of a node to <strong>True</strong> or <strong>False</strong> when <code>isLeaf</code> is <strong>False</strong>, and both are <strong>accepted</strong> in the answer.</p>

<p>A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:</p>

<ul>
	<li><code>val</code>: True if the node represents a grid of 1's or False if the node represents a grid of 0's.</li>
	<li><code>isLeaf</code>: True if the node is leaf node on the tree or False if the node has the four children.</li>
</ul>

<pre>class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;
}</pre>

<p>We can construct a Quad-Tree from a two-dimensional area using the following steps:</p>

<ol>
	<li>If the current grid has the same value (i.e all <code>1's</code> or all <code>0's</code>) set <code>isLeaf</code> True and set <code>val</code> to the value of the grid and set the four children to Null and stop.</li>
	<li>If the current grid has different values, set <code>isLeaf</code> to False and set <code>val</code> to any value and divide the current grid into four sub-grids as shown in the photo.</li>
	<li>Recurse for each of the children with the proper sub-grid.</li>
</ol>
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/11/new_top.png" style="width: 777px; height: 181px;">
<p>If you want to know more about the Quad-Tree, you can refer to the <a href="https://en.wikipedia.org/wiki/Quadtree">wiki</a>.</p>

<p><strong>Quad-Tree format:</strong></p>

<p>The output represents the serialized format of a Quad-Tree using level order traversal, where <code>null</code> signifies a path terminator where no node exists below.</p>

<p>It is very similar to the serialization of the binary tree. The only difference is that the node is represented as a list <code>[isLeaf, val]</code>.</p>

<p>If the value of <code>isLeaf</code> or <code>val</code> is True we represent it as <strong>1</strong> in the list <code>[isLeaf, val]</code> and if the value of <code>isLeaf</code> or <code>val</code> is False we represent it as <strong>0</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/11/grid1.png" style="width: 777px; height: 99px;">
<pre><strong>Input:</strong> grid = [[0,1],[1,0]]
<strong>Output:</strong> [[0,1],[1,0],[1,1],[1,1],[1,0]]
<strong>Explanation:</strong> The explanation of this example is shown below:
Notice that 0 represnts False and 1 represents True in the photo representing the Quad-Tree.
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/12/e1tree.png" style="width: 777px; height: 186px;">
</pre>

<p><strong>Example 2:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2020/02/12/e2mat.png" style="width: 777px; height: 343px;"></p>

<pre><strong>Input:</strong> grid = [[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,1,1,1,1],[1,1,1,1,1,1,1,1],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0]]
<strong>Output:</strong> [[0,1],[1,1],[0,1],[1,1],[1,0],null,null,null,null,[1,0],[1,0],[1,1],[1,1]]
<strong>Explanation:</strong> All values in the grid are not the same. We divide the grid into four sub-grids.
The topLeft, bottomLeft and bottomRight each has the same value.
The topRight have different values so we divide it into 4 sub-grids where each has the same value.
Explanation is shown in the photo below:
<img alt="" src="https://assets.leetcode.com/uploads/2020/02/12/e2tree.png" style="width: 777px; height: 328px;">
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == grid.length == grid[i].length</code></li>
	<li><code>n == 2<sup>x</sup></code> where <code>0 &lt;= x &lt;= 6</code></li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer/), [Tree](https://leetcode.com/tag/tree/), [Matrix](https://leetcode.com/tag/matrix/)

## Solution 1. Brute Force DFS

DFS for each branch of the tree

At first, we need to check our grid area has the same value

- Yes, then we count that as a whole, return a new Node with `isLeaf = True`
- No, then we split the area by 4, and then continue DFS each sub area

There is `N` row, and the grid is `N * N`

Time complexity is `O(N^2 \ log N)` since we have log N^2 levels, and in each level we visit N^2 cells at most, where grid is N x N matrix

In simple terms, if N is the size of an array and complexity of an algorithm is `N^2`, we can say that for each element we are traversing the entire array.

How we can convey the same thing here:

`n^2 * log(n^2) = n^2 * log(n)` => for each cell of grid, we traverse a logarithmic quarter of the grid cells

There are `N^2` cells in total, and each level we divide current cells in r1, c1, r2, c2 into 4 parts, so `4^k = N^2`, thus `k = log N^2` where the base is 4. At last log `N^2 = 2 * log N`

```py
# OJ: https://leetcode.com/problems/construct-quad-tree/
# Author: Duy Tran
# Time: O()
# Space: O()

"""
# Definition for a QuadTree node.
class Node:
    def __init__(self, val, isLeaf, topLeft, topRight, bottomLeft, bottomRight):
        self.val = val
        self.isLeaf = isLeaf
        self.topLeft = topLeft
        self.topRight = topRight
        self.bottomLeft = bottomLeft
        self.bottomRight = bottomRight
"""
class Solution:
    def isSame(self, grid, x, y, N):
        same = True
        for i in range(N):
            for j in range(N):
                same = grid[x][y] == grid[x + i][y + j]
                if not same: return False
        return True

    def dfs(self, grid, x, y, N):
        # Manual isSame method
        # same = True
        # for i in range(N):
        #     for j in range(N):
        #         same = grid[x][y] == grid[x + i][y + j]
        #         if not same: break
        #     else:
        #         continue
        #     break
        # print(same)
        if self.isSame(grid, x, y, N):
            return Node(grid[x][y], True)
        halfN = N // 2
        topLeft = self.dfs(grid, x, y, halfN)
        topRight = self.dfs(grid, x, y + halfN, halfN)
        bottomLeft = self.dfs(grid, x + halfN, y, halfN)
        bottomRight = self.dfs(grid, x + halfN, y + halfN, halfN)
        return Node(True, False, topLeft, topRight, bottomLeft, bottomRight)

    def construct(self, grid: List[List[int]]) -> 'Node':
        return self.dfs(grid, 0 , 0, len(grid))
```

## Solution 2. Brute Force DFS

There is `N` row, and the grid is `N * N`

`O(N^2)` time is because we actually look at each cell just once.

```py
# OJ: https://leetcode.com/problems/construct-quad-tree/
# Author: Duy Tran
# Time: O()
# Space: O()

"""
# Definition for a QuadTree node.
class Node:
    def __init__(self, val, isLeaf, topLeft, topRight, bottomLeft, bottomRight):
        self.val = val
        self.isLeaf = isLeaf
        self.topLeft = topLeft
        self.topRight = topRight
        self.bottomLeft = bottomLeft
        self.bottomRight = bottomRight
"""

class Solution:

    def dfs(self, grid, x, y, N):
        if N == 1:
            return Node(grid[x][y], True)

        res = Node()
        halfN = N // 2
        topLeft = self.dfs(grid, x, y, halfN)
        topRight = self.dfs(grid, x, y + halfN, halfN)
        bottomLeft = self.dfs(grid, x + halfN, y, halfN)
        bottomRight = self.dfs(grid, x + halfN, y + halfN, halfN)

        allLeaf = (topLeft.isLeaf and topRight.isLeaf and bottomLeft.isLeaf and bottomRight.isLeaf)
        sameVal = (topLeft.val == topRight.val and topRight.val == bottomLeft.val and bottomLeft.val == bottomRight.val)

        if allLeaf and sameVal:
            res.isLeaf = True;
            res.val = topLeft.val
        else:
            res.topLeft = topLeft
            res.topRight = topRight
            res.bottomLeft = bottomLeft
            res.bottomRight = bottomRight

        return res

    def construct(self, grid: List[List[int]]) -> 'Node':
        return self.dfs(grid, 0 , 0, len(grid))
```

## Solution 3. Non-recursive, Bottom-up

Forbidden Jutsu

Might cause brain damage.

Ref: https://leetcode.com/problems/construct-quad-tree/discuss/207275/Python-non-recursive-bottom-up-%3A-keep-reducing-by-factor-of-two

build an `N x N` array of Node class instances

then keep reducing the array size by a factor of 2 in both dimensions until only one Node class instance remains at `[0] [0]` index

```py
# OJ: https://leetcode.com/problems/construct-quad-tree/
# Author: Duy Tran
# Time: O()
# Space: O()

"""
# Definition for a QuadTree node.
class Node:
    def __init__(self, val, isLeaf, topLeft, topRight, bottomLeft, bottomRight):
        self.val = val
        self.isLeaf = isLeaf
        self.topLeft = topLeft
        self.topRight = topRight
        self.bottomLeft = bottomLeft
        self.bottomRight = bottomRight
"""

class Solution:
    def construct(self, grid: List[List[int]]) -> 'Node':
        N = len(grid)
        m = [[] for _ in range(N)]
        for i in range(N):
            for j in range(N):
                tmp = Node(grid[i][j] == 1, True)
                m[i].append(tmp)

        while N:
            N //= 2
            for i in range(N):
                for j in range(N):
                    a = m[i * 2][j * 2]
                    b = m[i * 2][j * 2 + 1]
                    c = m[i * 2 + 1][j * 2]
                    d = m[i * 2 + 1][j * 2 + 1]
                    print((i * 2),(j * 2))
                    print((i * 2),(j * 2 + 1))
                    print((i * 2 + 1),(j * 2))
                    print((i * 2 + 1),(j * 2 + 1))
                    print("next")

                    if a.val == b.val == c.val == d.val and a.val != '*':
                        m[i][j] = Node(a.val, True)
                    else:
                        m[i][j] = Node('*', False, a, b, c, d)
            print("end")
        return m[0][0]



```
