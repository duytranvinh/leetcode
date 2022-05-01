# [572. Subtree of Another Tree (Easy)](https://leetcode.com/problems/subtree-of-another-tree/)

<p>Given the roots of two binary trees <code>root</code> and <code>subRoot</code>, return <code>true</code> if there is a subtree of <code>root</code> with the same structure and node values of<code> subRoot</code> and <code>false</code> otherwise.</p>

<p>A subtree of a binary tree <code>tree</code> is a tree that consists of a node in <code>tree</code> and all of this node's descendants. The tree <code>tree</code> could also be considered as a subtree of itself.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg" style="width: 532px; height: 400px;">
<pre><strong>Input:</strong> root = [3,4,5,1,2], subRoot = [4,1,2]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg" style="width: 502px; height: 458px;">
<pre><strong>Input:</strong> root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the <code>root</code> tree is in the range <code>[1, 2000]</code>.</li>
	<li>The number of nodes in the <code>subRoot</code> tree is in the range <code>[1, 1000]</code>.</li>
	<li><code>-10<sup>4</sup> &lt;= root.val &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= subRoot.val &lt;= 10<sup>4</sup></code></li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Tree](https://leetcode.com/tag/tree/), [Depth-First Search](https://leetcode.com/tag/depth-first-search/), [String Matching](https://leetcode.com/tag/string-matching/), [Binary Tree](https://leetcode.com/tag/binary-tree/), [Hash Function](https://leetcode.com/tag/hash-function/)

**Similar Questions**:

- [Count Univalue Subtrees (Medium)](https://leetcode.com/problems/count-univalue-subtrees/)
- [Most Frequent Subtree Sum (Medium)](https://leetcode.com/problems/most-frequent-subtree-sum/)

## Solution 1. Recursive DFS

```py
# OJ: https://leetcode.com/problems/subtree-of-another-tree/
# Author: Duy Tran
# Time: O(MN) where M and N are the node count of Root and Sub.
# Space: O(H), height of the tree

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSame(self, root, sub):
        if not root and not sub:
            return True
        return root and sub and root.val == sub.val and self.isSame(root.left, sub.left) and self.isSame(root.right, sub.right)
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False
        if self.isSame(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

```

## Solution 2. Pre-order Serialize and KMP pattern match

For reference of KMP, look at question [28](/leetcode/28.%20Implement%20strStr%28%29)

```py
# OJ: https://leetcode.com/problems/subtree-of-another-tree/
# Author: Duy Tran
# Time: O(N + M), where N is the number of nodes in root, M is the number of nodes in subRoot
# Space: O(M)

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # Pre-order serialize for root and subRoot
    # Then use pattern matching KMP algorithm
    # to search subRoot in root
    def serialize(self, root):
        if not root:
            return ',#'
        return ',' + str(root.val) + self.serialize(root.left) + self.serialize(root.right)
    def getLPS(self, s):
        m, prev = len(s), 0
        lps = [0 for _ in s]
        for i in range(1, m):
            while s[i] != s[prev] and prev > 0:
                prev = lps[prev - 1]
            if s[i] == s[prev]:
                prev += 1
                lps[i] = prev
        return lps
    def kmp(self, s, p):
        lps = self.getLPS(p)
        # print(lps)
        n, m, j = len(s), len(p), 0
        for i in range(n):
            while s[i] != p[j] and j > 0:
                j = lps[j - 1]
            if s[i] == p[j]:
                j += 1
                if j == m: return True
        return False
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        s = self.serialize(root)
        p = self.serialize(subRoot)
        return self.kmp(s, p)
```
