# [40. Combination Sum II (Medium)](https://leetcode.com/problems/combination-sum-ii)

<p>Given a collection of candidate numbers (<code>candidates</code>) and a target number (<code>target</code>), find all unique combinations in <code>candidates</code>&nbsp;where the candidate numbers sum to <code>target</code>.</p>

<p>Each number in <code>candidates</code>&nbsp;may only be used <strong>once</strong> in the combination.</p>

<p><strong>Note:</strong>&nbsp;The solution set must not contain duplicate combinations.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> candidates = [10,1,2,7,6,1,5], target = 8
<strong>Output:</strong> 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> candidates = [2,5,2,1,2], target = 5
<strong>Output:</strong> 
[
[1,2,2],
[5]
]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;candidates.length &lt;= 100</code></li>
	<li><code>1 &lt;=&nbsp;candidates[i] &lt;= 50</code></li>
	<li><code>1 &lt;= target &lt;= 30</code></li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Meta](https://leetcode.com/company/facebook), [Google](https://leetcode.com/company/google), [TikTok](https://leetcode.com/company/tiktok), [Microsoft](https://leetcode.com/company/microsoft), [Adobe](https://leetcode.com/company/adobe), [Oracle](https://leetcode.com/company/oracle), [Uber](https://leetcode.com/company/uber), [Airbnb](https://leetcode.com/company/airbnb), [Apple](https://leetcode.com/company/apple), [Snap](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Backtracking](https://leetcode.com/tag/backtracking)

**Similar Questions**:

- [Combination Sum (Medium)](https://leetcode.com/problems/combination-sum)

## Solution 1. DFS/Backtracking

Since the requirement ask **The solution set must not contain duplicate combinations.** so we need to sort the array first. Once the array is sorted, we can check `i` and `i+1` to skip duplicate.

Sort the array

We go backtracking IN ORDER from left to right

At each recursive

1. If we reach the target, we add the current path into the result

2. If we went out of bound, then we return as no need to go further

3. If there are still a chance to continue, we do both as below:

   - Add the CURRENT `i` number to the continue the path
   - Pop the CURRENT `i` number and then
   - Use while loop to check `arr[i]` and arr[i+1] to skip duplicate
   - Add the NEXT number to continue the path

```py
# OJ: https://leetcode.com/problems/combination-sum-ii
# Author: Duy Tran
# Time: O(N2^2)
# Space: O(N)

class Solution:
    def combinationSum2(self, arr: List[int], target: int) -> List[List[int]]:
        res = []
        n = len(arr)
        arr.sort()

        def dfs(i, cur, total):
          if total == target:
            res.append(cur.copy())
            return
          if i == n or total > target:
            return
          # include arr[i]
          cur.append(arr[i])
          dfs(i + 1, cur, total + arr[i])
          cur.pop()
          # skip arr[i]
          while i + 1 < n and arr[i] == arr[i+1]:
            i += 1
          dfs(i + 1, cur, total)

        dfs(0, [], 0)
        return res
```

Javascript

```js
/**
 * @param {number[]} arr
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function (arr, target) {
  const res = [];
  const n = arr.length;
  arr.sort((a, b) => a - b);

  const dfs = (i, cur, total) => {
    if (total === target) {
      res.push([...cur]);
      return;
    }
    if (i === n || total > target) {
      return;
    }
    // include arr[i]
    cur.push(arr[i]);
    dfs(i + 1, cur, total + arr[i]);
    cur.pop();

    // skip arr[i]
    while (i + 1 < n && arr[i] === arr[i + 1]) {
      i++;
    }
    dfs(i + 1, cur, total);
  };

  dfs(0, [], 0);
  return res;
};
```

## Solution 2. Stack

The limit of the recursion is the recursive stack might get limited.

We can optimize a bit using a stack method

```py
class Solution:
    def combinationSum2(self, arr, target):
        res = []
        arr.sort()
        n = len(arr)
        stack = [(0, [], 0)]  # stack stores tuples of (index, current combination, current total)

        while stack:
            i, cur, total = stack.pop()
            if total == target:
                res.append(cur)
                continue
            while i < n and total <= target:
                if total + arr[i] > target:
                    break
                # Add the current element to the current combination
                stack.append((i + 1, cur + [arr[i]], total + arr[i]))
                # Skip duplicates
                while i + 1 < n and arr[i] == arr[i + 1]:
                    i += 1
                i += 1
        return res
```

```js
/**
 * @param {number[]} arr
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function (arr, target) {
  const res = [];
  arr.sort((a, b) => a - b);
  const n = arr.length;
  const stack = [[0, [], 0]]; // stack stores [index, current combination, current total]
  while (stack.length > 0) {
    const [i, cur, total] = stack.pop();
    if (total === target) {
      res.push(cur);
      continue;
    }
    let j = i;
    while (j < n && total <= target) {
      if (total + arr[j] > target) {
        break;
      }
      // Add the current element to the current combination
      stack.push([j + 1, [...cur, arr[j]], total + arr[j]]);
      // Skip duplicates
      while (j + 1 < n && arr[j] === arr[j + 1]) {
        j++;
      }
      j++;
    }
  }
  return res;
};
```
