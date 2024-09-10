# [39. Combination Sum (Medium)](https://leetcode.com/problems/combination-sum)

<p>Given an array of <strong>distinct</strong> integers <code>candidates</code> and a target integer <code>target</code>, return <em>a list of all <strong>unique combinations</strong> of </em><code>candidates</code><em> where the chosen numbers sum to </em><code>target</code><em>.</em> You may return the combinations in <strong>any order</strong>.</p>

<p>The <strong>same</strong> number may be chosen from <code>candidates</code> an <strong>unlimited number of times</strong>. Two combinations are unique if the <span data-keyword="frequency-array">frequency</span> of at least one of the chosen numbers is different.</p>

<p>The test cases are generated such that the number of unique combinations that sum up to <code>target</code> is less than <code>150</code> combinations for the given input.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2,3,6,7], target = 7
<strong>Output:</strong> [[2,2,3],[7]]
<strong>Explanation:</strong>
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2,3,5], target = 8
<strong>Output:</strong> [[2,2,2,2],[2,3,3],[3,5]]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2], target = 1
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= candidates.length &lt;= 30</code></li>
	<li><code>2 &lt;= candidates[i] &lt;= 40</code></li>
	<li>All elements of <code>candidates</code> are <strong>distinct</strong>.</li>
	<li><code>1 &lt;= target &lt;= 40</code></li>
</ul>

**Companies**:
[Airbnb](https://leetcode.com/company/airbnb), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Oracle](https://leetcode.com/company/oracle), [Walmart Labs](https://leetcode.com/company/walmart-labs), [ByteDance](https://leetcode.com/company/bytedance), [TikTok](https://leetcode.com/company/tiktok), [Meta](https://leetcode.com/company/facebook), [Yahoo](https://leetcode.com/company/yahoo), [Apple](https://leetcode.com/company/apple), [Zoho](https://leetcode.com/company/zoho), [LinkedIn](https://leetcode.com/company/linkedin), [J.P. Morgan](https://leetcode.com/company/jpmorgan), [Salesforce](https://leetcode.com/company/salesforce), [Adobe](https://leetcode.com/company/adobe), [eBay](https://leetcode.com/company/ebay), [Snap](https://leetcode.com/company/snapchat), [Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Backtracking](https://leetcode.com/tag/backtracking)

**Similar Questions**:

- [Letter Combinations of a Phone Number (Medium)](https://leetcode.com/problems/letter-combinations-of-a-phone-number)
- [Combination Sum II (Medium)](https://leetcode.com/problems/combination-sum-ii)
- [Combinations (Medium)](https://leetcode.com/problems/combinations)
- [Combination Sum III (Medium)](https://leetcode.com/problems/combination-sum-iii)
- [Factor Combinations (Medium)](https://leetcode.com/problems/factor-combinations)
- [Combination Sum IV (Medium)](https://leetcode.com/problems/combination-sum-iv)
- [The Number of Ways to Make the Sum (Medium)](https://leetcode.com/problems/the-number-of-ways-to-make-the-sum)

## Solution 1. DFS/Backtracking

<p><img src="https://assets.leetcode.com/static_assets/media/original_images/39/39_zoom_in.png"></p>

We go backtracking IN ORDER from left to right

At each recursive

1. If we reach the target, we add the current path into the result

2. If we went out of bound, then we return as no need to go further

3. If there are still a chance to continue, we do both as below:

   - Add the CURRENT `i` number to the continue the path

   - Pop the CURRENT `i` number and then
   - Add the NEXT `i+1` number to continue the path

Python

```py
# OJ: https://leetcode.com/problems/combination-sum
# Author: Duy Tran
# Time: O(N)
# Space: O(N), for the recursion stack

class Solution:
    def combinationSum(self, arr: List[int], target: int) -> List[List[int]]:
        res = []
        n = len(arr)

        def dfs(i, cur, total):
          if total == target:
              res.append(cur.copy())
              return
          if i >= n or total > target:
              return

          cur.append(arr[i])
          dfs(i, cur, total + arr[i])
          cur.pop()
          dfs(i + 1, cur, total)

        dfs(0, [], 0)
        return res
```

Javascript

```js
/**
 * OJ: https://leetcode.com/problems/combination-sum
 * Author: Duy Tran
 * Time: O(N)
 * Space: O(N), for the recursion stack
 */

/**
 * @param {number[]} arr
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (arr, target) {
  const res = [];
  const n = arr.length;
  const dfs = (i, cur, total) => {
    if (total === target) {
      res.push([...cur]);
      return;
    }
    if (i >= n || total > target) {
      return;
    }

    cur.push(arr[i]);
    dfs(i, cur, total + arr[i]);
    cur.pop();
    dfs(i + 1, cur, total);
  };
  dfs(0, [], 0);
  return res;
};
```
