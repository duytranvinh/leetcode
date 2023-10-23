# [70. Climbing Stairs (Easy)](https://leetcode.com/problems/climbing-stairs)

<p>You are climbing a staircase. It takes <code>n</code> steps to reach the top.</p>

<p>Each time you can either climb <code>1</code> or <code>2</code> steps. In how many distinct ways can you climb to the top?</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 45</code></li>
</ul>


**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [Apple](https://leetcode.com/company/apple), [Yahoo](https://leetcode.com/company/yahoo), [Zoho](https://leetcode.com/company/zoho), [Accenture](https://leetcode.com/company/accenture), [Uber](https://leetcode.com/company/uber), [Facebook](https://leetcode.com/company/facebook), [Swiggy](https://leetcode.com/company/swiggy), [Microsoft](https://leetcode.com/company/microsoft), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Qualcomm](https://leetcode.com/company/qualcomm), [Expedia](https://leetcode.com/company/expedia), [Oracle](https://leetcode.com/company/oracle), [Grammarly](https://leetcode.com/company/grammarly), [Intel](https://leetcode.com/company/intel), [Visa](https://leetcode.com/company/visa), [Accolite](https://leetcode.com/company/accolite), [Yandex](https://leetcode.com/company/yandex), [Nagarro](https://leetcode.com/company/nagarro), [Autodesk](https://leetcode.com/company/autodesk)

**Related Topics**:  
[Math](https://leetcode.com/tag/math), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming), [Memoization](https://leetcode.com/tag/memoization)

**Similar Questions**:
* [Min Cost Climbing Stairs (Easy)](https://leetcode.com/problems/min-cost-climbing-stairs)
* [Fibonacci Number (Easy)](https://leetcode.com/problems/fibonacci-number)
* [N-th Tribonacci Number (Easy)](https://leetcode.com/problems/n-th-tribonacci-number)
* [Minimum Rounds to Complete All Tasks (Medium)](https://leetcode.com/problems/minimum-rounds-to-complete-all-tasks)
* [Count Number of Ways to Place Houses (Medium)](https://leetcode.com/problems/count-number-of-ways-to-place-houses)
* [Number of Ways to Reach a Position After Exactly k Steps (Medium)](https://leetcode.com/problems/number-of-ways-to-reach-a-position-after-exactly-k-steps)
* [Count Ways To Build Good Strings (Medium)](https://leetcode.com/problems/count-ways-to-build-good-strings)
* [Frog Jump II (Medium)](https://leetcode.com/problems/frog-jump-ii)

**Hints**:
* To reach nth step, what could have been your previous steps? (Think about the step sizes)

## Solution 1.

Bottom up DP

`climbStairs(n) = climbStairs(n-1) + climbStairs(n-2)`

Base case `climbStairs(0) = 1` and `climbStairs(1) = 1`

Similar to Fibonacci

```py
# OJ: https://leetcode.com/problems/climbing-stairs
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def climbStairs(self, n: int) -> int:
        prev, cur = 0, 1
        while(n):
            next = cur + prev
            prev = cur
            cur = next
            n -= 1
        return cur

```

Javascript

```js
// # OJ: https://leetcode.com/problems/climbing-stairs
// # Author: Duy Tran
// # Time: O(N)
// # Space: O(1)

/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    let prev = 0;
    let cur = 1;
    while (n) {
        const next = cur + prev;
        prev = cur;
        cur = next;
        n--;
    }
    return cur
};
```