# [966. Vowel Spellchecker (Medium)](https://leetcode.com/problems/vowel-spellchecker)

<p>Given a <code>wordlist</code>, we want to implement a spellchecker that converts a query word into a correct word.</p>

<p>For a given <code>query</code> word, the spell checker handles two categories of spelling mistakes:</p>

<ul>
	<li>Capitalization: If the query matches a word in the wordlist (<strong>case-insensitive</strong>), then the query word is returned with the same case as the case in the wordlist.

	<ul>
		<li>Example: <code>wordlist = [&quot;yellow&quot;]</code>, <code>query = &quot;YellOw&quot;</code>: <code>correct = &quot;yellow&quot;</code></li>
		<li>Example: <code>wordlist = [&quot;Yellow&quot;]</code>, <code>query = &quot;yellow&quot;</code>: <code>correct = &quot;Yellow&quot;</code></li>
		<li>Example: <code>wordlist = [&quot;yellow&quot;]</code>, <code>query = &quot;yellow&quot;</code>: <code>correct = &quot;yellow&quot;</code></li>
	</ul>
	</li>
	<li>Vowel Errors: If after replacing the vowels <code>(&#39;a&#39;, &#39;e&#39;, &#39;i&#39;, &#39;o&#39;, &#39;u&#39;)</code> of the query word with any vowel individually, it matches a word in the wordlist (<strong>case-insensitive</strong>), then the query word is returned with the same case as the match in the wordlist.
	<ul>
		<li>Example: <code>wordlist = [&quot;YellOw&quot;]</code>, <code>query = &quot;yollow&quot;</code>: <code>correct = &quot;YellOw&quot;</code></li>
		<li>Example: <code>wordlist = [&quot;YellOw&quot;]</code>, <code>query = &quot;yeellow&quot;</code>: <code>correct = &quot;&quot;</code> (no match)</li>
		<li>Example: <code>wordlist = [&quot;YellOw&quot;]</code>, <code>query = &quot;yllw&quot;</code>: <code>correct = &quot;&quot;</code> (no match)</li>
	</ul>
	</li>
</ul>

<p>In addition, the spell checker operates under the following precedence rules:</p>

<ul>
	<li>When the query exactly matches a word in the wordlist (<strong>case-sensitive</strong>), you should return the same word back.</li>
	<li>When the query matches a word up to capitlization, you should return the first such match in the wordlist.</li>
	<li>When the query matches a word up to vowel errors, you should return the first such match in the wordlist.</li>
	<li>If the query has no matches in the wordlist, you should return the empty string.</li>
</ul>

<p>Given some <code>queries</code>, return a list of words <code>answer</code>, where <code>answer[i]</code> is the correct word for <code>query = queries[i]</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> wordlist = ["KiTe","kite","hare","Hare"], queries = ["kite","Kite","KiTe","Hare","HARE","Hear","hear","keti","keet","keto"]
<strong>Output:</strong> ["kite","KiTe","KiTe","Hare","hare","","","KiTe","","KiTe"]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> wordlist = ["yellow"], queries = ["YellOw"]
<strong>Output:</strong> ["yellow"]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= wordlist.length, queries.length &lt;= 5000</code></li>
	<li><code>1 &lt;= wordlist[i].length, queries[i].length &lt;= 7</code></li>
	<li><code>wordlist[i]</code> and <code>queries[i]</code> consist only of only English letters.</li>
</ul>


**Companies**:
[Grammarly](https://leetcode.com/company/grammarly), [Thumbtack](https://leetcode.com/company/thumbtack)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [String](https://leetcode.com/tag/string)

## Solution 1. Building hashmap

Build 3 different hashmap for each case `perfect`, `cap`, and `vowel`

Check every `w` in `queries`, then check in order `perfect`, `cap`, `vowel`

Python: `cap` and `vowel` run wordlist backward so that the FIRST MATCH will override any "same" case

```py

# OJ: https://leetcode.com/problems/vowel-spellchecker
# Author: Duy Tran
# Time: O(M + N)
# Space: O(M)
# M is length of wordlist, N is length of queries

class Solution:
    def spellchecker(self, wordlist: List[str], queries: List[str]) -> List[str]:
      def devowel(word):
            return "".join('*' if c in 'aeiou' else c
                           for c in word)
      perfect = {w: w for w in wordlist}
      # cap and vowel run backward so that the FIRST MATCH will override any "same" case
      cap = {w.lower(): w for w in wordlist[::-1]}
      vowel = {devowel(w.lower()): w for w in wordlist[::-1]}

      return [(perfect.get(w) or cap.get(w.lower()) or vowel.get(devowel(w.lower())) or "") for w in queries]
```

Javascript


```js
/**
 * @param {string[]} wordlist
 * @param {string[]} queries
 * @return {string[]}
 */
var spellchecker = function(wordlist, queries) {
    const devowel = (w) => (w.replace(/[aeiou]/g, '*'));
    perfect = new Map();
    cap = new Map();
    vowel = new Map();
    for (const w of wordlist) {
      !perfect.has(w) && perfect.set(w, w);
      const lower = w.toLowerCase();
      !cap.has(lower) && cap.set(lower, w);
      !vowel.has(devowel(lower)) && vowel.set(devowel(lower), w);
    }

    return queries.map(w => {
      const lower = w.toLowerCase();
      return perfect.get(w) || cap.get(lower) || vowel.get(devowel(lower)) || ''
    });
};
```