# [12. Integer to Roman (Medium)](https://leetcode.com/problems/integer-to-roman/)

<p>Roman numerals are represented by seven different symbols:&nbsp;<code>I</code>, <code>V</code>, <code>X</code>, <code>L</code>, <code>C</code>, <code>D</code> and <code>M</code>.</p>

<pre><strong>Symbol</strong>       <strong>Value</strong>
I             1
V             5
X             10
L             50
C             100
D             500
M             1000</pre>

<p>For example,&nbsp;<code>2</code> is written as <code>II</code>&nbsp;in Roman numeral, just two one's added together. <code>12</code> is written as&nbsp;<code>XII</code>, which is simply <code>X + II</code>. The number <code>27</code> is written as <code>XXVII</code>, which is <code>XX + V + II</code>.</p>

<p>Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not <code>IIII</code>. Instead, the number four is written as <code>IV</code>. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as <code>IX</code>. There are six instances where subtraction is used:</p>

<ul>
	<li><code>I</code> can be placed before <code>V</code> (5) and <code>X</code> (10) to make 4 and 9.&nbsp;</li>
	<li><code>X</code> can be placed before <code>L</code> (50) and <code>C</code> (100) to make 40 and 90.&nbsp;</li>
	<li><code>C</code> can be placed before <code>D</code> (500) and <code>M</code> (1000) to make 400 and 900.</li>
</ul>

<p>Given an integer, convert it to a roman numeral.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> num = 3
<strong>Output:</strong> "III"
<strong>Explanation:</strong> 3 is represented as 3 ones.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> num = 58
<strong>Output:</strong> "LVIII"
<strong>Explanation:</strong> L = 50, V = 5, III = 3.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> num = 1994
<strong>Output:</strong> "MCMXCIV"
<strong>Explanation:</strong> M = 1000, CM = 900, XC = 90 and IV = 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= num &lt;= 3999</code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Capital One](https://leetcode.com/company/capital-one), [tiktok](https://leetcode.com/company/tiktok)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [Math](https://leetcode.com/tag/math/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:

- [Roman to Integer (Easy)](https://leetcode.com/problems/roman-to-integer/)
- [Integer to English Words (Hard)](https://leetcode.com/problems/integer-to-english-words/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/integer-to-roman/
# Author: Duy Tran
# Time: O(1)
# Space: O(1)

class Solution:
    def intToRoman(self, num: int) -> str:
        # check max num, here is 3999
        symbols = 'MDCLXVI'
        values = [1000, 500, 100, 50, 10, 5, 1]
        res = list()
        # i = 0, 2, 4, 6
        for i in range(0, 7, 2):
            d = int(num / values[i])
            # d = 0,1,2,3,4,5,6,7,8,9
            # if d = 0: num < symbols[i]
            # if d <= 3: III => add symbols[i] d times
            # if d == 4: IV => add symbols[i] and symbols[i - 1]
            # if d == 5: V => add symbols[i - 1]
            # if  5 < d <= 8: VIII => add symbols[i - 1] then add symbols[i] (d - 5) times
            # if d == 9: IX => add symbols[i] then add symbols[i - 2]
            if d == 0: continue
            if d <= 3:
                while d:
                    res.append(symbols[i])
                    d -= 1
            elif d == 4:
                res.append(symbols[i])
                res.append(symbols[i - 1])
            elif d == 5:
                res.append(symbols[i - 1])
            elif d <= 8:
                res.append(symbols[i - 1])
                while d > 5:
                    res.append(symbols[i])
                    d -= 1
            else:
                res.append(symbols[i])
                res.append(symbols[i - 2])
            num %= values[i]
        return ''.join(res)
```
