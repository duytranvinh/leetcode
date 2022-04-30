# [819. Most Common Word (Easy)](https://leetcode.com/problems/most-common-word/)

<p>Given a string <code>paragraph</code> and a string array of the banned words <code>banned</code>, return <em>the most frequent word that is not banned</em>. It is <strong>guaranteed</strong> there is <strong>at least one word</strong> that is not banned, and that the answer is <strong>unique</strong>.</p>

<p>The words in <code>paragraph</code> are <strong>case-insensitive</strong> and the answer should be returned in <strong>lowercase</strong>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
<strong>Output:</strong> "ball"
<strong>Explanation:</strong> 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> paragraph = "a.", banned = []
<strong>Output:</strong> "a"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= paragraph.length &lt;= 1000</code></li>
	<li>paragraph consists of English letters, space <code>' '</code>, or one of the symbols: <code>"!?',;."</code>.</li>
	<li><code>0 &lt;= banned.length &lt;= 100</code></li>
	<li><code>1 &lt;= banned[i].length &lt;= 10</code></li>
	<li><code>banned[i]</code> consists of only lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Counting](https://leetcode.com/tag/counting/)

## Solution 1. Build dictionary

```py
# OJ: https://leetcode.com/problems/most-common-word/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
# Build a dictionary of words
# Filter those banned words
# Return the most common word
    def mostCommonWord(self, p: str, banned: List[str]) -> str:
        m = defaultdict(int)
        i = 0
        n = len(p)
        s = str()
        for c in p:
            #if it's an alphabet, keep building s
            if c.isalpha():
                s += c.lower()
            #if not, reset s
            else:
                #if s is a completed word
                #add it into map
                if s.isalpha():
                    m[s] += 1
                s = ""
        # Add last word into the map
        if p[-1].isalpha(): m[s] += 1
        # Filter those banned words
        for b in banned: m[b] = 0
        # Find the best count
        res = str()
        count = 0
        for w in m:
            if m[w] > count:
                res = w
                count = m[w]
        return res
        for b in banned: m[b] = 0

```

## Solution 2. Clean data first then build dictionary

```py
# OJ: https://leetcode.com/problems/most-common-word/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

# change to lowercase
# remove all punctuations
# split words
# words count for each word not in banned set
# return the most common word
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        # convert to all lowercase
        paragraph = paragraph.lower()
        # remove special characters
        for c in paragraph:
            if not c.isalpha():
                paragraph = paragraph.replace(c, " ")
        # split paragraph into words
        words = paragraph.split()
        m = defaultdict(int)
        # tally each word
        for word in words:
            if word not in banned:
                m[word] += 1
        count = 0
        res = ""
        # Find the word with the highest occurance that is not banned
        for (word, curCnt) in m.items():
            if curCnt > count:
                count = curCnt
                res = word
        return res
                m[word] += 1
```
