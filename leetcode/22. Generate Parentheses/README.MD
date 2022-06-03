# [22. Generate Parentheses (Medium)](https://leetcode.com/problems/generate-parentheses/)

<p>Given <code>n</code> pairs of parentheses, write a function to <em>generate all combinations of well-formed parentheses</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> ["((()))","(()())","(())()","()(())","()()()"]
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> ["()"]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 8</code></li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Uber](https://leetcode.com/company/uber), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [C3 IoT](https://leetcode.com/company/c3-iot), [Oracle](https://leetcode.com/company/oracle), [ByteDance](https://leetcode.com/company/bytedance), [Huawei](https://leetcode.com/company/huawei), [Grab](https://leetcode.com/company/grab)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/), [Backtracking](https://leetcode.com/tag/backtracking/)

**Similar Questions**:

- [Letter Combinations of a Phone Number (Medium)](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
- [Valid Parentheses (Easy)](https://leetcode.com/problems/valid-parentheses/)
- [Check if a Parentheses String Can Be Valid (Medium)](https://leetcode.com/problems/check-if-a-parentheses-string-can-be-valid/)

## Solution 1. Backtracking

Only add open parenthesis if open < n

Only add a closing parenthesis if closed < open

valid IF `open == close == n`

```py

# OJ: https://leetcode.com/problems/generate-parentheses/
# Author: Duy Tran
# Time: O(C(N))
# Space: O(N)

class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        stack = list()
        res = list()
        def backtracking(openN, closedN):
            if openN == closedN == n:
                res.append("".join(stack))
                return
            if openN < n:
                stack.append("(")
                backtracking(openN + 1, closedN)
                stack.pop()
            if closedN < openN:
                stack.append(")")
                backtracking(openN, closedN + 1)
                stack.pop()
        backtracking(0, 0)
        return res

```

## Solution 2. Bit Manipulation

NOT SUFFICIENT

We generate every possible of the parenthesis and check if each is valid

In term of time complexity, it's N^2.

```py
# OJ: https://leetcode.com/problems/generate-parentheses/
# Author: Duy Tran
# Time: O(N^2)
# Space: O(N)

class Solution:
    def getBit(self, n, i): #get bit of n at position i
        return (n >> i) & 1

    def isValid(self, s):
        cnt = 0
        for c in s:
            if c == '(':
                cnt += 1
                if cnt > len(s) >> 1:   return False
            if c == ')':
                cnt -= 1
                if cnt < 0:             return False
        return cnt == 0

    def generateParenthesis(self, n: int) -> List[str]:
        res = list()
        k = 2 * n
        m = 1 << k
        for i in range(m):
            r = list()
            for j in range(k):
                if self.getBit(i, j) == 1:
                    r.append('(')
                else:
                    r.append(')')
            if self.isValid(r):
                res.append("".join(r))
        return res
```
