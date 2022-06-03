# [78. Subsets (Medium)](https://leetcode.com/problems/subsets/)

<p>Given an integer array <code>nums</code> of <strong>unique</strong> elements, return <em>all possible subsets (the power set)</em>.</p>

<p>The solution set <strong>must not</strong> contain duplicate subsets. Return the solution in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [[],[0]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>All the numbers of&nbsp;<code>nums</code> are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Twitter](https://leetcode.com/company/twitter), [tiktok](https://leetcode.com/company/tiktok), [Reddit](https://leetcode.com/company/reddit), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Oracle](https://leetcode.com/company/oracle), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [Visa](https://leetcode.com/company/visa)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Backtracking](https://leetcode.com/tag/backtracking/), [Bit Manipulation](https://leetcode.com/tag/bit-manipulation/)

**Similar Questions**:

- [Subsets II (Medium)](https://leetcode.com/problems/subsets-ii/)
- [Generalized Abbreviation (Medium)](https://leetcode.com/problems/generalized-abbreviation/)
- [Letter Case Permutation (Medium)](https://leetcode.com/problems/letter-case-permutation/)
- [Find Array Given Subset Sums (Hard)](https://leetcode.com/problems/find-array-given-subset-sums/)
- [Count Number of Maximum Bitwise-OR Subsets (Medium)](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets/)

## Before we start

There is `2^N` subsets

Each subset could be length of `N`

So no matter of what we do, the best Time Complexity is `O(N * 2^N)`

## Solution 1. Backtracking (DFS)

```py
# OJ: https://leetcode.com/problems/subsets/
# Author: Duy Tran
# Time: O(N * 2^N)
# Space: O(N)

class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        subset = []
        def dfs(i):
            if i >= len(nums):
                res.append(subset.copy())
                return
            # the path where we include nums[i]
            subset.append(nums[i])
            dfs(i + 1)
            # the path where we NOT include nums[i]
            subset.pop()
            dfs(i + 1)
        dfs(0)
        return res

```

## Solution 2. DP

Using `[1, 2, 3]` as an example, the iterative process is like:

Initially, one empty subset `[[]]`

Adding 1 to `[]`: `[[], [1]]`

Adding 2 to `[]` and `[1]`: `[[], [1], [2], [1, 2]]`

Adding 3 to `[]`, `[1]`, `[2]` and `[1, 2]`: `[[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]`

```py
# OJ: https://leetcode.com/problems/subsets/
# Author: Duy Tran
# Time: O(N * 2^N)
# Space: O(N) or O(1) since we don't use any extra spaces rather than the result

class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = list()
        res.append([])
        for num in nums:
            n = len(res)
            for i in range(n):
                res.append(res[i].copy())
                res[-1].append(num)
        return res
```

## Solution 3. Bit Manipulation

To give all the possible subsets, we just need to exhaust all the possible combinations of the numbers. And each number has only two possibilities: either in or not in a subset. And this can be represented using a bit.

Using `[1, 2, 3]` as an example, `1` appears once in every two consecutive subsets, `2` appears twice in every four consecutive subsets, and `3` appears four times in every eight subsets (initially all subsets are empty):

```
[], [ ], [ ], [    ], [ ], [    ], [    ], [       ]
[], [1], [ ], [1   ], [ ], [1   ], [    ], [1      ]
[], [1], [2], [1, 2], [ ], [1   ], [2   ], [1, 2   ]
[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]
```

```
n = 0

    1 0, 1

    2 00, 01, 10, 11

    3 000, 001, 010, 011, 100, 101, 110, 111

      000 001 020 021 300 301 320 321
```

`n` must be < 20

```py
# OJ: https://leetcode.com/problems/subsets/
# Author: Duy Tran
# Time: O(N * 2^N)
# Space: O(1)

class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        def getBit(n, i):  #get bit of n at position i
            return (n >> i) & 1
        res = list()
        m = 1 << n
        for i in range(m):
            r = list()
            for j in range(n):
                if getBit(i, j) == 1:
                    r.append(nums[j])
            res.append(r)
        return res
```
