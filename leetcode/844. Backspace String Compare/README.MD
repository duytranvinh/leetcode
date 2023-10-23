# [844. Backspace String Compare (Easy)](https://leetcode.com/problems/backspace-string-compare)

<p>Given two strings <code>s</code> and <code>t</code>, return <code>true</code> <em>if they are equal when both are typed into empty text editors</em>. <code>&#39;#&#39;</code> means a backspace character.</p>

<p>Note that after backspacing an empty text, the text will continue empty.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;ab#c&quot;, t = &quot;ad#c&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> Both s and t become &quot;ac&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;ab##&quot;, t = &quot;c#d#&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> Both s and t become &quot;&quot;.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;a#c&quot;, t = &quot;b&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> s becomes &quot;c&quot; while t becomes &quot;b&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code><span>1 &lt;= s.length, t.length &lt;= 200</span></code></li>
	<li><span><code>s</code> and <code>t</code> only contain lowercase letters and <code>&#39;#&#39;</code> characters.</span></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you solve it in <code>O(n)</code> time and <code>O(1)</code> space?</p>


**Companies**:
[Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Oracle](https://leetcode.com/company/oracle), [Grammarly](https://leetcode.com/company/grammarly), [Microsoft](https://leetcode.com/company/microsoft), [IBM](https://leetcode.com/company/ibm), [Booking.com](https://leetcode.com/company/bookingcom), [Apple](https://leetcode.com/company/apple), [Visa](https://leetcode.com/company/visa), [Bloomberg](https://leetcode.com/company/bloomberg), [VMware](https://leetcode.com/company/vmware), [Twilio](https://leetcode.com/company/twilio), [TikTok](https://leetcode.com/company/tiktok)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers), [String](https://leetcode.com/tag/string), [Stack](https://leetcode.com/tag/stack), [Simulation](https://leetcode.com/tag/simulation)

**Similar Questions**:
* [Crawler Log Folder (Easy)](https://leetcode.com/problems/crawler-log-folder)
* [Removing Stars From a String (Medium)](https://leetcode.com/problems/removing-stars-from-a-string)

## Solution 1. Stack

```py
# OJ: https://leetcode.com/problems/backspace-string-compare
# Author: Duy Tran
# Time: O(M + N)
# Space: O(M + N)

class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def build(st):
            r = list()
            for c in st:
                if c != '#':
                    r.append(c)
                elif r: # r not empty
                    r.pop()
            return "".join(r)
        return build(s) == build(t)

```

Javascript

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    const build = (st) => {
        const r = new Array();
        for (const c of st) {
            if (c !== '#') {
                r.push(c);
            } else if (r.length > 0) {
                r.pop()
            }
        }
        return  r.join('');
    }
    return build(s) === build(t);
};
```

## Solution 2. Two pointer

Going reverse is better so we know `#` to skip

```py
# OJ: https://leetcode.com/problems/backspace-string-compare
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        i, j = len(s) -1, len(t) - 1
        backS = backT = 0
        while i >= 0 or j >= 0:
            while i >= 0 and (backS or s[i] == '#'):
                backS += 1 if s[i] == '#' else -1
                i -= 1
            while j >= 0 and (backT or  t[j] =='#'):
                backT += 1 if t[j] == '#' else -1
                j -= 1
            if (i >= 0 and j >= 0 and s[i] == t[j]):
                i -= 1
                j -= 1
            else:
                break
        return i == j == -1
```

Also Python but Vip pro

`reduce()` in Python take `(fnc, seq, initial)`

```py
class Solution:
    def backspaceCompare(self, S, T):
        back = lambda res, c: res[:-1] if c == '#' else res + c
        return reduce(back, S, "") == reduce(back, T, "")
```

Javscript

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    let i = s.length - 1, j = t.length - 1, back = 0;
    while (i >= 0 || j >= 0) {
        back = 0;
        while (i >= 0 && (back || s[i] === '#')) {
            back += s[i] === '#' ? 1 : -1;
            i--;
        }
        back = 0;
        while (j >= 0 && (back || t[j] === '#')) {
            back += t[j] === '#' ? 1 : -1;
            j--;
        }
        if (i >= 0 && j >= 0 && s[i] === t[j]) {
            i--;
            j--;
        } else {
            break;
        }
    }
    return i === -1 && j === -1
};
```