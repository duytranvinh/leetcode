# [118. Pascal's Triangle (Easy)](https://leetcode.com/problems/pascals-triangle)

<p>Given an integer <code>numRows</code>, return the first numRows of <strong>Pascal&#39;s triangle</strong>.</p>

<p>In <strong>Pascal&#39;s triangle</strong>, each number is the sum of the two numbers directly above it as shown:</p>
<img alt="" src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif" style="height:240px; width:260px" />
<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> numRows = 5
<strong>Output:</strong> [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> numRows = 1
<strong>Output:</strong> [[1]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= numRows &lt;= 30</code></li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Microsoft](https://leetcode.com/company/microsoft), [Yahoo](https://leetcode.com/company/yahoo), [Facebook](https://leetcode.com/company/facebook), [Adobe](https://leetcode.com/company/adobe), [HSBC](https://leetcode.com/company/hsbc), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [tcs](https://leetcode.com/company/tcs), [persistent systems](https://leetcode.com/company/persistent-systems), [Oracle](https://leetcode.com/company/oracle), [Twitter](https://leetcode.com/company/twitter)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming)

**Similar Questions**:

- [Pascal's Triangle II (Easy)](https://leetcode.com/problems/pascals-triangle-ii)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/pascals-triangle
# Author: Duy Tran
# Time: O(N^2)
# Space: O(N^2)

class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        res = []
        for n in range(numRows):
          cur = []
          for i in range(n+1):
            if i == 0 or i == n:
              cur.append(1)
            else:
              a = res[n-1][i-1]
              b = res[n-1][i]
              cur.append(a+b)
          res.append(cur)
        return res

```
