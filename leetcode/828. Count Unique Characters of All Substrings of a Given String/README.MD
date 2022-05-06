# [828. Count Unique Characters of All Substrings of a Given String (Hard)](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/)

<p>Let's define a function <code>countUniqueChars(s)</code> that returns the number of unique characters on <code>s</code>.</p>

<ul>
	<li>For example, calling <code>countUniqueChars(s)</code> if <code>s = "LEETCODE"</code> then <code>"L"</code>, <code>"T"</code>, <code>"C"</code>, <code>"O"</code>, <code>"D"</code> are the unique characters since they appear only once in <code>s</code>, therefore <code>countUniqueChars(s) = 5</code>.</li>
</ul>

<p>Given a string <code>s</code>, return the sum of <code>countUniqueChars(t)</code> where <code>t</code> is a substring of <code>s</code>.</p>

<p>Notice that some substrings can be repeated so in this case you have to count the repeated ones too.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "ABC"
<strong>Output:</strong> 10
<strong>Explanation: </strong>All possible substrings are: "A","B","C","AB","BC" and "ABC".
Every substring is composed with only unique letters.
Sum of lengths of all substring is 1 + 1 + 1 + 2 + 2 + 3 = 10
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "ABA"
<strong>Output:</strong> 8
<strong>Explanation: </strong>The same as example 1, except <code>countUniqueChars</code>("ABA") = 1.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = "LEETCODE"
<strong>Output:</strong> 92
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> consists of uppercase English letters only.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:

- [Total Appeal of A String (Hard)](https://leetcode.com/problems/total-appeal-of-a-string/)

## Solution 1. Brute Force (Time Limit Exceeded)

Loop through every substring
Count each substring

- If count == 1, which means unique char
- If count == 2, which means NOT unique
- If two == 26, which means 26 char in the English alphabet is used more than once

Case: `ABC`
Run:

1. `ABC`
   1. `A`: prev = 1
   2. `AB`: prev = 3 (1 + 2) for case where `B` and `AB`
   3. `ABC`: prev = 6 (3 + 3) for case where `C`, `BC`, `ABC`
2. `BC`
   1. `B`: prev = 1
   2. `BC`: prev = 3 for case where `C` and `BC`
3. `C`
   1. `C`: prev = 1

Total of this is: 10

```py
# OJ: https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)
# Ref: https://github.com/lzl124631x/LeetCode/tree/master/leetcode/828.%20Unique%20Letter%20String

class Solution:
    def uniqueLetterString(self, s: str) -> int:
        n = len(s)
        res = 0
        for i in range(n):
            cnt = defaultdict(int)
            prev = 0
            two = 0
            tmp = str()
            for j in range(i, n):
                if two >= 26: break
                c = s[j]
                tmp += c
                cnt[c] += 1
                cur = prev
                if cnt[c] == 1: cur += 1
                elif cnt[c] == 2:
                    cur -= 1
                    two += 2
                res += cur
                prev = cur
        return res
                elif cnt[c] == 2:

```

## Solution 2. DP

We have the formula that `dp[i] = dp[i-1] + (i - j) - (j - k)`.

We can transform to the following formula: `res[i] = prev + (i - j) - (j - k)` with `i = [0, n)`

Our `idx` or `dp` will store [last, second last] appear

Default `j` and `k` is `-1`

**Example** `ABCDAEA`

`A`

`B`, `AB`

`C`, `BC`, `ABC`

`D`, `CD`, `BCD`, `ABCD`

`A`, `DA`, `CDA`, `BCDA`, `ABCDA`

`A`, `EA`, `AEA`, `DAEA`, `CDAEA`, `BCDAEA`

`A`, `EA`, `AEA`, `DAEA`, `CDAEA`, `BCDAEA`, `ABCDAEA`

We have:

`idx[char] = [-1, -1]`

`idx[s[0]] = [0, -1]`

`prev`, `res` = 1

1. `i` = 1 => `AB`
   - `res += prev + (i - j) - (j - k)`
   - `res += 1 + (1 - (-1)) - (-1 - (-1))`
   - `res += 1 + (1 + 1) - (-1 + 1)`
   - `res += 1 + 2 - 0`
     - `+2` here because `B` appear `2` more time
     - in `B` and `AB`
     - Because `A` is "reused" so we have to `prev = 1` into our equation
   - `res += 3`
   - `res` = `4` and `prev` = `3`
2. `i` = 2 => `ABC`

   - `res += prev + (i - j) - (j - k)`
   - `res += prev + (2 + 1) - 0`
   - `res += prev + 3 - 0`
     - `+3` here because `C` appear `3` more time
     - in `C`, `BC`, and `ABC`
     - Because `A` and `B` is "reused" so we have to `prev = 3` into our equation
   - `res += 6`
   - `res` = `10` and `prev` = `6`

3. `i` = 3 => `ABCD`

   - `res += prev + (i - j) - (j - k)`
   - `res += prev + (3 + 1) - 0`
   - `res += (prev = 6) + 4 - 0`
     - `+4` here because `D` appear `4` more time
     - in `D`, `CD`, `BCD` and `ABCD`
     - Because `A`, `B` and `C` is "reused" so we have to `prev = 6` into our equation
   - `res += 10`
   - `res` = `20` and `prev` = `10`

4. `i` = 4 => `ABCDA`

   - `idx[A] = [0, -1]`
   - `i = 4`, `j = 0`, `k = -1`
   - `res += prev + (i - j) - (j - k)`
   - `res += 10 + (4 - 0) - (0 - (-1))`
     - 5 case is added `A`, `DA`, `CDA`, `BCDA`, `ABCDA`
     - From `(0, 4]`, there are 4 new case `A`, `DA`, `CDA`, `BCDA`
     - With `prev` and a new `A` in the equation, there are 4 new cases where `A` is not unique: `ABCDA`. Therefore we `-1` here
   - `res += 10 + 4 - 1`
   - `res += 13`
   - `res` = `33` and `prev` = `13`
   - `idx[A]` = `[4, 0]`

5. `i` = 5 => `ABCDAE`

   - `res += 13 + (5 + 1) - 0`
   - `res += 19`
   - `res` = `52` and `prev` = `19`

6. `i` = 6 => `ABCDAEA`
   - `idx[A]` = `[4, 0]`
   - `res += 19 + (6 - 4) - (4 - 0)`
   - `res += 19 + 2 - 4`
     - 7 cases are added `A`, `EA`, `AEA`, `DAEA`, `CDAEA`, `BCDAEA`, `ABCDAEA`
     - From `(4,6]`, there are 2 cases `A` and `EA`
     - With `prev` and a new `A` in the equation, there are 4 new cases where `A` is not unique: `AEA`, `DAEA`, `CDAEA`, `BCDAEA`
     - Case `ABCDAEA` is already invalid `A`, so adding a new `A` don't change it count
   - `res += 17`
   - `res` = `69` and `prev` = `17`

```py
# OJ: https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/
# Author: Duy Tran
# Time: O(N)
# Space: O(1), 26 english characters only

class Solution:
    def uniqueLetterString(self, s: str) -> int:
        if len(s) == 0: return 0
        idx = defaultdict(lambda: [-1,-1])
        idx[s[0]][0] = 0
        res, prev = 1,1
        for i in range(1,len(s)):
            char = s[i]
            j,k = idx[char]
            curr = prev + (i-j) - (j-k)
            res += curr
            prev = curr
            idx[char][1] = idx[char][0]
            idx[char][0] = i
        return res
```
