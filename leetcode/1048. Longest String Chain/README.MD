# [1048. Longest String Chain (Medium)](https://leetcode.com/problems/longest-string-chain/)

<p>You are given an array of <code>words</code> where each word consists of lowercase English letters.</p>

<p><code>word<sub>A</sub></code> is a <strong>predecessor</strong> of <code>word<sub>B</sub></code> if and only if we can insert <strong>exactly one</strong> letter anywhere in <code>word<sub>A</sub></code> <strong>without changing the order of the other characters</strong> to make it equal to <code>word<sub>B</sub></code>.</p>

<ul>
	<li>For example, <code>"abc"</code> is a <strong>predecessor</strong> of <code>"ab<u>a</u>c"</code>, while <code>"cba"</code> is not a <strong>predecessor</strong> of <code>"bcad"</code>.</li>
</ul>

<p>A <strong>word chain</strong><em> </em>is a sequence of words <code>[word<sub>1</sub>, word<sub>2</sub>, ..., word<sub>k</sub>]</code> with <code>k &gt;= 1</code>, where <code>word<sub>1</sub></code> is a <strong>predecessor</strong> of <code>word<sub>2</sub></code>, <code>word<sub>2</sub></code> is a <strong>predecessor</strong> of <code>word<sub>3</sub></code>, and so on. A single word is trivially a <strong>word chain</strong> with <code>k == 1</code>.</p>

<p>Return <em>the <strong>length</strong> of the <strong>longest possible word chain</strong> with words chosen from the given list of </em><code>words</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["a","b","ba","bca","bda","bdca"]
<strong>Output:</strong> 4
<strong>Explanation</strong>: One of the longest word chains is ["a","<u>b</u>a","b<u>d</u>a","bd<u>c</u>a"].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["xbc","pcxbcf","xb","cxbc","pcxbc"]
<strong>Output:</strong> 5
<strong>Explanation:</strong> All the words can be put in a word chain ["xb", "xb<u>c</u>", "<u>c</u>xbc", "<u>p</u>cxbc", "pcxbc<u>f</u>"].
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> words = ["abcd","dbqca"]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The trivial word chain ["abcd"] is one of the longest word chains.
["abcd","dbqca"] is not a valid word chain because the ordering of the letters is changed.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 1000</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 16</code></li>
	<li><code>words[i]</code> only consists of lowercase English letters.</li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Oracle](https://leetcode.com/company/oracle), [tiktok](https://leetcode.com/company/tiktok), [Flipkart](https://leetcode.com/company/flipkart)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

## Solution 1. DP with DFS and Memorization

1. Initial a set `wordSet` with all the words in the `words`

2. Initial hash map `wordChain` with `key = word` and `value = chain-length`

3. Iterate over the list. For each word in the list perform a depth-first search.

4. In the DFS, consider the current word `w` as the last word in the word sequence.

   1. If `w` was seen before in `wordChain`, return `wordChain[w]`

   2. Initialize `maxLength` to 1. Because this chain original have length of 1 which contain only `w`

   3. Iterate over the entire length of the `w`

      - Create all possible words `w1` by taking out one character at a time.

      - If `w1` is in our `wordSet`, then we perform `dfs(w1)`

      - Update `maxLength = max(maxLength, dfs(w1) + 1)`

   4. Set the `wordChain[w] = maxLength`

   5. Return `maxLength`

5. Update `res = max(res, dfs(w))`

6. Return `res`

**Complexity**

We perform a DFS for each word `O(N)`

For each word, we iterate over its length `O(L)`

At each index `i` we create a new word by deleting the character at position i from the original word `O(L)`

```py
# OJ: https://leetcode.com/problems/longest-string-chain/
# Author: Duy Tran
# Time: O(N * L^2), L is max length of word
# Space: O(N)

class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        wordSet = set(words)
        wordChain = dict() # "word": chain-length
        def dfs(w):
            if w in wordChain:
                return wordChain[w]
            maxLength = 1
            for i in range(len(w)):
                w1 = w[0:i] + w[i+1:]
                if w1 not in wordSet: continue
                maxLength = max(maxLength, dfs(w1) + 1)
            wordChain[w] = maxLength
            return maxLength
        res = 0
        for w in words:
            res = max(res, dfs(w))
        return res

```
