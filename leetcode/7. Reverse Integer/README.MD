# [7. Reverse Integer (Medium)](https://leetcode.com/problems/reverse-integer/)

<p>Given a signed 32-bit integer <code>x</code>, return <code>x</code><em> with its digits reversed</em>. If reversing <code>x</code> causes the value to go outside the signed 32-bit integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then return <code>0</code>.</p>

<p><strong>Assume the environment does not allow you to store 64-bit integers (signed or unsigned).</strong></p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> x = 123
<strong>Output:</strong> 321
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> x = -123
<strong>Output:</strong> -321
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> x = 120
<strong>Output:</strong> 21
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= x &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

**Companies**:  
[Adobe](https://leetcode.com/company/adobe), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Oracle](https://leetcode.com/company/oracle), [Bloomberg](https://leetcode.com/company/bloomberg), [Apple](https://leetcode.com/company/apple), [Visa](https://leetcode.com/company/visa), [American Express](https://leetcode.com/company/american-express), [Samsung](https://leetcode.com/company/samsung)

**Related Topics**:  
[Math](https://leetcode.com/tag/math/)

**Similar Questions**:

- [String to Integer (atoi) (Medium)](https://leetcode.com/problems/string-to-integer-atoi/)
- [Reverse Bits (Easy)](https://leetcode.com/problems/reverse-bits/)
- [A Number After a Double Reversal (Easy)](https://leetcode.com/problems/a-number-after-a-double-reversal/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/reverse-integer/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def reverse(self, x: int) -> int:
        res = 0
        negative = False
        if x < 0:
            negative = True
            x = -x
        while x:
            r = x % 10
            res = res * 10 + r
            if res < -2**31 or res >= 2**31:
                return 0
            x = int(x / 10)
        return -res if negative else res
```
