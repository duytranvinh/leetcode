# [58. Length of Last Word (Easy)](https://leetcode.com/problems/length-of-last-word)

<p>Given a string <code>s</code> consisting of words and spaces, return <em>the length of the <strong>last</strong> word in the string.</em></p>

<p>A <strong>word</strong> is a maximal <span data-keyword="substring-nonempty">substring</span> consisting of non-space characters only.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;Hello World&quot;
<strong>Output:</strong> 5
<strong>Explanation:</strong> The last word is &quot;World&quot; with length 5.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;   fly me   to   the moon  &quot;
<strong>Output:</strong> 4
<strong>Explanation:</strong> The last word is &quot;moon&quot; with length 4.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;luffy is still joyboy&quot;
<strong>Output:</strong> 6
<strong>Explanation:</strong> The last word is &quot;joyboy&quot; with length 6.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> consists of only English letters and spaces <code>&#39; &#39;</code>.</li>
	<li>There will be at least one word in <code>s</code>.</li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber)

**Related Topics**:  
[String](https://leetcode.com/tag/string)

## Solution 1.

Run from reverse. Counting from backward.

If there is a space, and we already start counting, then that is the end of last word, return the count

```py
# OJ: https://leetcode.com/problems/length-of-last-word
# Author: Duy Tran
# Time: O(N)
# Space: O(1)


class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        res = 0
        for i in s[::-1]:
          if i == " ":
            if res > 0: return res
          else:
            res += 1
        return res

```
