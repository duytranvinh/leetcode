# [49. Group Anagrams (Medium)](https://leetcode.com/problems/group-anagrams)

<p>Given an array of strings <code>strs</code>, group <strong>the anagrams</strong> together. You can return the answer in <strong>any order</strong>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> strs = ["eat","tea","tan","ate","nat","bat"]
<strong>Output:</strong> [["bat"],["nat","tan"],["ate","eat","tea"]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> strs = [""]
<strong>Output:</strong> [[""]]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> strs = ["a"]
<strong>Output:</strong> [["a"]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 100</code></li>
	<li><code>strs[i]</code> consists of lowercase English letters.</li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Facebook](https://leetcode.com/company/facebook), [Adobe](https://leetcode.com/company/adobe), [ServiceNow](https://leetcode.com/company/servicenow), [Google](https://leetcode.com/company/google), [Yandex](https://leetcode.com/company/yandex), [Zoho](https://leetcode.com/company/zoho), [Salesforce](https://leetcode.com/company/salesforce), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Nvidia](https://leetcode.com/company/nvidia), [Bloomberg](https://leetcode.com/company/bloomberg), [Yahoo](https://leetcode.com/company/yahoo), [Visa](https://leetcode.com/company/visa), [Oracle](https://leetcode.com/company/oracle), [EPAM Systems](https://leetcode.com/company/epam-systems), [Affirm](https://leetcode.com/company/affirm), [Atlassian](https://leetcode.com/company/atlassian), [TikTok](https://leetcode.com/company/tiktok), [Autodesk](https://leetcode.com/company/autodesk), [Palo Alto Networks](https://leetcode.com/company/palo-alto-networks), [PayPal](https://leetcode.com/company/paypal), [Uber](https://leetcode.com/company/uber), [eBay](https://leetcode.com/company/ebay), [Walmart Labs](https://leetcode.com/company/walmart-labs), [JPMorgan](https://leetcode.com/company/jpmorgan), [Tesla](https://leetcode.com/company/tesla), [Nutanix](https://leetcode.com/company/nutanix), [Expedia](https://leetcode.com/company/expedia), [SIG](https://leetcode.com/company/sig), [Intuit](https://leetcode.com/company/intuit), [Samsung](https://leetcode.com/company/samsung), [VMware](https://leetcode.com/company/vmware), [MathWorks](https://leetcode.com/company/mathworks), [Snapchat](https://leetcode.com/company/snapchat), [Twilio](https://leetcode.com/company/twilio), [BlackRock](https://leetcode.com/company/blackrock), [Cruise Automation](https://leetcode.com/company/cruise-automation), [Avalara](https://leetcode.com/company/avalara), [Zoom](https://leetcode.com/company/zoom), [Faire](https://leetcode.com/company/faire), [Veeva](https://leetcode.com/company/veeva), [Rivian](https://leetcode.com/company/rivian), [Yelp](https://leetcode.com/company/yelp)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [String](https://leetcode.com/tag/string), [Sorting](https://leetcode.com/tag/sorting)

**Similar Questions**:

- [Valid Anagram (Easy)](https://leetcode.com/problems/valid-anagram)
- [Group Shifted Strings (Medium)](https://leetcode.com/problems/group-shifted-strings)
- [Find Resultant Array After Removing Anagrams (Easy)](https://leetcode.com/problems/find-resultant-array-after-removing-anagrams)
- [Count Anagrams (Hard)](https://leetcode.com/problems/count-anagrams)

## Solution 1.

Use hashmap to keep track of each possible anagrams

Sort each word to be the key of hashmap

![49_groupanagrams1](https://leetcode.com/problems/group-anagrams/Figures/49_groupanagrams1.png)

```py
# OJ: https://leetcode.com/problems/group-anagrams
# Author: Duy Tran
# Time: O(N K log K) where N is the length of arr, and K is the maximum length of a string
# Space: O(N K)


class Solution:
    def groupAnagrams(self, arr: List[str]) -> List[List[str]]:
        res = defaultdict(list)
        for s in arr:
          cur = tuple(sorted(s))
          res[cur].append(s)
        return res.values()

```

## Solution 2.

Sorting costing too much, use an array of character (26 chars only) to keep track of it.

```py
# OJ: https://leetcode.com/problems/group-anagrams
# Author: Duy Tran
# Time: O(N K)
# Space: O(N K)

class Solution:
    def groupAnagrams(self, arr: List[str]) -> List[List[str]]:
        res = defaultdict(list)
        for s in arr:
          count = [0] * 26
          for c in s:
            count[ord(c) - ord('a')] += 1
          res[tuple(count)].append(s)
        return res.values()
```
