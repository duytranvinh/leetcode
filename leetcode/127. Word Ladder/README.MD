# [127. Word Ladder (Hard)](https://leetcode.com/problems/word-ladder/)

<p>A <strong>transformation sequence</strong> from word <code>beginWord</code> to word <code>endWord</code> using a dictionary <code>wordList</code> is a sequence of words <code>beginWord -&gt; s<sub>1</sub> -&gt; s<sub>2</sub> -&gt; ... -&gt; s<sub>k</sub></code> such that:</p>

<ul>
	<li>Every adjacent pair of words differs by a single letter.</li>
	<li>Every <code>s<sub>i</sub></code> for <code>1 &lt;= i &lt;= k</code> is in <code>wordList</code>. Note that <code>beginWord</code> does not need to be in <code>wordList</code>.</li>
	<li><code>s<sub>k</sub> == endWord</code></li>
</ul>

<p>Given two words, <code>beginWord</code> and <code>endWord</code>, and a dictionary <code>wordList</code>, return <em>the <strong>number of words</strong> in the <strong>shortest transformation sequence</strong> from</em> <code>beginWord</code> <em>to</em> <code>endWord</code><em>, or </em><code>0</code><em> if no such sequence exists.</em></p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
<strong>Output:</strong> 5
<strong>Explanation:</strong> One shortest transformation sequence is "hit" -&gt; "hot" -&gt; "dot" -&gt; "dog" -&gt; cog", which is 5 words long.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= beginWord.length &lt;= 10</code></li>
	<li><code>endWord.length == beginWord.length</code></li>
	<li><code>1 &lt;= wordList.length &lt;= 5000</code></li>
	<li><code>wordList[i].length == beginWord.length</code></li>
	<li><code>beginWord</code>, <code>endWord</code>, and <code>wordList[i]</code> consist of lowercase English letters.</li>
	<li><code>beginWord != endWord</code></li>
	<li>All the words in <code>wordList</code> are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [LinkedIn](https://leetcode.com/company/linkedin), [Microsoft](https://leetcode.com/company/microsoft), [Qualtrics](https://leetcode.com/company/qualtrics), [Apple](https://leetcode.com/company/apple), [Snapchat](https://leetcode.com/company/snapchat), [Lyft](https://leetcode.com/company/lyft), [Adobe](https://leetcode.com/company/adobe), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Yahoo](https://leetcode.com/company/yahoo), [ByteDance](https://leetcode.com/company/bytedance)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Breadth-First Search](https://leetcode.com/tag/breadth-first-search/)

**Similar Questions**:

- [Word Ladder II (Hard)](https://leetcode.com/problems/word-ladder-ii/)
- [Minimum Genetic Mutation (Medium)](https://leetcode.com/problems/minimum-genetic-mutation/)

## Solution 1. BFS

Since we are looking for the shortest path, BFS should be our first option.

We form a pattern for each word: `dog = ['*og', 'd*g', 'do*']`

We find the `neighbor` / `edges` of each patern

`edges['do*'] = [dog, dot]`

**Time Complexity**

We have `n = len(wordList)` with all words are same size, so `m = len(word)`

We have visit `n` words, check each `m` neighbors, then add copy them to our queue

=> Time: `O(N * M * M)` => `O(N * M^2)`

We store our `neighbor` hashmap with the size `O(N * M)`

```py
# OJ: https://leetcode.com/problems/word-ladder/
# Author: Duy Tran
# Time: O(N * M^2)
# Space: O(N * M)

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList:
            return 0
        m = len(beginWord)
        wordList.append(beginWord)
        n = len(wordList)
        edges = collections.defaultdict(list)

        for word in wordList:
            for i in range(m):
                pattern = word[:i] + "*" + word[i + 1:]
                edges[pattern].append(word)

        visited = set([beginWord])
        q = [beginWord]
        res = 1
        while q:
            for _ in range(len(q)):
                word = q.pop(0)
                if word == endWord:
                    return res
                for i in range(m):
                    pattern = word[:i] + "*" + word[i + 1:]
                    for e in edges[pattern]:
                        if e in visited:
                            continue
                        visited.add(e)
                        q.append(e)
            res += 1
        return 0

```
