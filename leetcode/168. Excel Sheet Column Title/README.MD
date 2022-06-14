# [168. Excel Sheet Column Title (Easy)](https://leetcode.com/problems/excel-sheet-column-title/)

<p>Given an integer <code>columnNumber</code>, return <em>its corresponding column title as it appears in an Excel sheet</em>.</p>

<p>For example:</p>

<pre>A -&gt; 1
B -&gt; 2
C -&gt; 3
...
Z -&gt; 26
AA -&gt; 27
AB -&gt; 28 
...
</pre>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> columnNumber = 1
<strong>Output:</strong> "A"
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> columnNumber = 28
<strong>Output:</strong> "AB"
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> columnNumber = 701
<strong>Output:</strong> "ZY"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= columnNumber &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Math](https://leetcode.com/tag/math/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:

- [Excel Sheet Column Number (Easy)](https://leetcode.com/problems/excel-sheet-column-number/)
- [Cells in a Range on an Excel Sheet (Easy)](https://leetcode.com/problems/cells-in-a-range-on-an-excel-sheet/)

## Solution 1.

[Reference](https://leetcode.com/problems/excel-sheet-column-title/discuss/51404/Python-solution-with-explanation)

```py
# OJ: https://leetcode.com/problems/excel-sheet-column-title/
# Author: Duy Tran
# Time: O(logN)
# Space: O(1)

class Solution:
    def convertToTitle(self, n: int) -> str:
        res = list()
        distance = ord('A')
        while n > 0:
            y = (n-1) % 26
            n = (n-1) // 26
            s = chr(y+distance)
            res.append(s)
        res.reverse()
        return ''.join(res)

```
