# [125. Valid Palindrome (Easy)](https://leetcode.com/problems/valid-palindrome/)

<p>A phrase is a <strong>palindrome</strong> if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.</p>

<p>Given a string <code>s</code>, return <code>true</code><em> if it is a <strong>palindrome</strong>, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s = "A man, a plan, a canal: Panama"
<strong>Output:</strong> true
<strong>Explanation:</strong> "amanaplanacanalpanama" is a palindrome.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s = "race a car"
<strong>Output:</strong> false
<strong>Explanation:</strong> "raceacar" is not a palindrome.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> s = " "
<strong>Output:</strong> true
<strong>Explanation:</strong> s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>s</code> consists only of printable ASCII characters.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Bloomberg](https://leetcode.com/company/bloomberg), [LinkedIn](https://leetcode.com/company/linkedin), [Wayfair](https://leetcode.com/company/wayfair), [Spotify](https://leetcode.com/company/spotify), [ServiceNow](https://leetcode.com/company/servicenow), [JPMorgan](https://leetcode.com/company/jpmorgan), [American Express](https://leetcode.com/company/american-express)

**Related Topics**:  
[Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/)

**Similar Questions**:

- [Palindrome Linked List (Easy)](https://leetcode.com/problems/palindrome-linked-list/)
- [Valid Palindrome II (Easy)](https://leetcode.com/problems/valid-palindrome-ii/)
- [Maximum Product of the Length of Two Palindromic Subsequences (Medium)](https://leetcode.com/problems/maximum-product-of-the-length-of-two-palindromic-subsequences/)
- [Find First Palindromic String in the Array (Easy)](https://leetcode.com/problems/find-first-palindromic-string-in-the-array/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/valid-palindrome/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = s.lower()
        l, r = 0, len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l] != s[r]:
                return False
            l += 1
            r -= 1
        return True

    #Custom function to check, but dont need
    def alphanum(self, c):
        return ord('a') <= ord(c) <= ord('z') or ord('0') <= ord(c) <= ord('9')

```
