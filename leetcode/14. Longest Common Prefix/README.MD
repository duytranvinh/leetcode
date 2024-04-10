# [14. Longest Common Prefix (Easy)](https://leetcode.com/problems/longest-common-prefix)

<p>Write a function to find the longest common prefix string amongst an array of strings.</p>

<p>If there is no common prefix, return an empty string <code>&quot;&quot;</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> strs = [&quot;flower&quot;,&quot;flow&quot;,&quot;flight&quot;]
<strong>Output:</strong> &quot;fl&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> strs = [&quot;dog&quot;,&quot;racecar&quot;,&quot;car&quot;]
<strong>Output:</strong> &quot;&quot;
<strong>Explanation:</strong> There is no common prefix among the input strings.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 200</code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 200</code></li>
	<li><code>strs[i]</code> consists of only lowercase English letters.</li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Facebook](https://leetcode.com/company/facebook), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [Uber](https://leetcode.com/company/uber), [Yahoo](https://leetcode.com/company/yahoo), [Zoho](https://leetcode.com/company/zoho), [Cognizant](https://leetcode.com/company/cognizant), [Accenture](https://leetcode.com/company/accenture), [turing](https://leetcode.com/company/turing), [IBM](https://leetcode.com/company/ibm), [Microsoft](https://leetcode.com/company/microsoft), [SAP](https://leetcode.com/company/sap), [Salesforce](https://leetcode.com/company/salesforce), [Accolite](https://leetcode.com/company/accolite), [PornHub](https://leetcode.com/company/pornhub), [Expedia](https://leetcode.com/company/expedia), [Visa](https://leetcode.com/company/visa), [Walmart Labs](https://leetcode.com/company/walmart-labs), [tcs](https://leetcode.com/company/tcs), [Oracle](https://leetcode.com/company/oracle), [Cisco](https://leetcode.com/company/cisco), [Capital One](https://leetcode.com/company/capital-one), [Roblox](https://leetcode.com/company/roblox), [Intel](https://leetcode.com/company/intel), [Yelp](https://leetcode.com/company/yelp)

**Related Topics**:  
[String](https://leetcode.com/tag/string), [Trie](https://leetcode.com/tag/trie)

**Similar Questions**:

- [Smallest Missing Integer Greater Than Sequential Prefix Sum (Easy)](https://leetcode.com/problems/smallest-missing-integer-greater-than-sequential-prefix-sum)
- [Find the Length of the Longest Common Prefix (Medium)](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix)
- [Longest Common Suffix Queries (Hard)](https://leetcode.com/problems/longest-common-suffix-queries)

## Solution 1.

Take the first word out to be the sample

Loop through each char in the sample

For each char, check if it match with other words in the array

If it is not, or it reach the end in one of the other words, return the current result

```py
# OJ: https://leetcode.com/problems/longest-common-prefix
# Author: Duy Tran
# Time: O(M * N), M is length of first word and N is length of array
# Space: O(1)

class Solution:
    def longestCommonPrefix(self, arr: List[str]) -> str:
      res = ""
      sample = arr[0]
      for i in range(len(sample)):
        for w in arr:
          if i == len(w) or w[i] != sample[i]:
            return res
        res += sample[i]
      return res

```
