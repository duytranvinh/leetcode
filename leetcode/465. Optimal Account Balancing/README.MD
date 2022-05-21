# [465. Optimal Account Balancing (Hard)](https://leetcode.com/problems/optimal-account-balancing/)

<p>You are given an array of transactions <code>transactions</code> where <code>transactions[i] = [from<sub>i</sub>, to<sub>i</sub>, amount<sub>i</sub>]</code> indicates that the person with <code>ID = from<sub>i</sub></code> gave <code>amount<sub>i</sub> $</code> to the person with <code>ID = to<sub>i</sub></code>.</p>

<p>Return <em>the minimum number of transactions required to settle the debt</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> transactions = [[0,1,10],[2,0,5]]
<strong>Output:</strong> 2
<strong>Explanation:</strong>
Person #0 gave person #1 $10.
Person #2 gave person #0 $5.
Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> transactions = [[0,1,10],[1,0,1],[1,2,5],[2,0,5]]
<strong>Output:</strong> 1
<strong>Explanation:</strong>
Person #0 gave person #1 $10.
Person #1 gave person #0 $1.
Person #1 gave person #2 $5.
Person #2 gave person #0 $5.
Therefore, person #1 only need to give person #0 $4, and all debt is settled.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= transactions.length &lt;= 8</code></li>
	<li><code>transactions[i].length == 3</code></li>
	<li><code>0 &lt;= from<sub>i</sub>, to<sub>i</sub> &lt; 12</code></li>
	<li><code>from<sub>i</sub> != to<sub>i</sub></code></li>
	<li><code>1 &lt;= amount<sub>i</sub> &lt;= 100</code></li>
</ul>

**Companies**:  
[Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google), [Affirm](https://leetcode.com/company/affirm)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Backtracking](https://leetcode.com/tag/backtracking/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/), [Bitmask](https://leetcode.com/tag/bitmask/)

## Solution 1. Recursion, DFS

[Reference](https://leetcode.com/problems/optimal-account-balancing/discuss/130895/Recursion-Logical-Thinking)

Build up the debt array

Then we DFS

```py
# OJ: https://leetcode.com/problems/optimal-account-balancing/
# Author: Duy Tran
# Time:  O(N!)
# Space: O(N)

class Solution:
    def buildDebt(self, trans):
        m = defaultdict(int)
        for giver, taker, amount in trans:
            m[giver] += amount
            m[taker] -= amount
        return [amount for amount in m.values() if amount != 0]

    def dfs(self, debt, cur):
        n = len(debt)
        while (cur < n and debt[cur] == 0):
            cur += 1

        if cur == n:
            return 0

        res = float('inf')
        for i in range(cur + 1, n):
            if debt[i] * debt[cur] < 0:
                debt[i] += debt[cur]
                res = min(res, self.dfs(debt, cur + 1) + 1)
                debt[i] -= debt[cur]
        return res

    def minTransfers(self, transactions: List[List[int]]) -> int:
        debt = self.buildDebt(transactions)
        return self.dfs(debt, 0)

```
