# [72. Edit Distance (Hard)](https://leetcode.com/problems/edit-distance/)

<p>Given two strings <code>word1</code> and <code>word2</code>, return <em>the minimum number of operations required to convert <code>word1</code> to <code>word2</code></em>.</p>

<p>You have the following three operations permitted on a word:</p>

<ul>
	<li>Insert a character</li>
	<li>Delete a character</li>
	<li>Replace a character</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> word1 = "horse", word2 = "ros"
<strong>Output:</strong> 3
<strong>Explanation:</strong> 
horse -&gt; rorse (replace 'h' with 'r')
rorse -&gt; rose (remove 'r')
rose -&gt; ros (remove 'e')
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> word1 = "intention", word2 = "execution"
<strong>Output:</strong> 5
<strong>Explanation:</strong> 
intention -&gt; inention (remove 't')
inention -&gt; enention (replace 'i' with 'e')
enention -&gt; exention (replace 'n' with 'x')
exention -&gt; exection (replace 'n' with 'c')
exection -&gt; execution (insert 'u')
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= word1.length, word2.length &lt;= 500</code></li>
	<li><code>word1</code> and <code>word2</code> consist of lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [LinkedIn](https://leetcode.com/company/linkedin), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Rubrik](https://leetcode.com/company/rubrik)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:

- [One Edit Distance (Medium)](https://leetcode.com/problems/one-edit-distance/)
- [Delete Operation for Two Strings (Medium)](https://leetcode.com/problems/delete-operation-for-two-strings/)
- [Minimum ASCII Delete Sum for Two Strings (Medium)](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/)
- [Uncrossed Lines (Medium)](https://leetcode.com/problems/uncrossed-lines/)
- [Minimum White Tiles After Covering With Carpets (Hard)](https://leetcode.com/problems/minimum-white-tiles-after-covering-with-carpets/)

## Solution 1. DP

We initially our `dp` 2D array with `col = word1` and `row = word2`

We make one extra row and col at the begin

This `dp` array mean that at `dp[i][j]`, it is the number of number operation to transform `word1[:j-1]` to `word2[:i-1]`

When we traverse our `dp`, there are only two scenarios

1. `word2[i - 1] == word1[j - 1]`. In this case, we don't need to do extra operation here. So we update `dp[i][j] = dp[i - 1][j - 1]`

2. `word2[i - 1] != word1[j - 1]`. In this case, we need to do extra operation here. So we need to find the minimum number of operations in our past in the left, top, top-left cell. So we update `dp[i][j] = 1 + min(dp[i - 1][j - 1], dp[i][j - 1], dp[i - 1][j])`

   - Insert: `dp[i][j - 1]`

   - Delete: `dp[i - 1][j]`

   - Replace: `dp[i - 1][j - 1]`

We return `dp[-1][-1]` as it's our last operation

```py
# OJ: https://leetcode.com/problems/edit-distance/
# Author: Duy Tran
# Time: O(MN)
# Space: O(MN)

class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        n = len(word1)
        m = len(word2)
        dp = [[x for x in range(n + 1)] for y in range(m + 1)]

        for i in range(1, m + 1):
            dp[i][0] = dp[i - 1][0] + 1


        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if word2[i - 1] == word1[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = 1 + min(dp[i - 1][j - 1], dp[i][j - 1], dp[i - 1][j])
                print(dp)

        return dp[-1][-1]

```
