# [1268. Search Suggestions System (Medium)](https://leetcode.com/problems/search-suggestions-system/)

<p>You are given an array of strings <code>products</code> and a string <code>searchWord</code>.</p>

<p>Design a system that suggests at most three product names from <code>products</code> after each character of <code>searchWord</code> is typed. Suggested products should have common prefix with <code>searchWord</code>. If there are more than three products with a common prefix return the three lexicographically minimums products.</p>

<p>Return <em>a list of lists of the suggested products after each character of </em><code>searchWord</code><em> is typed</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> products = ["mobile","mouse","moneypot","monitor","mousepad"], searchWord = "mouse"
<strong>Output:</strong> [
["mobile","moneypot","monitor"],
["mobile","moneypot","monitor"],
["mouse","mousepad"],
["mouse","mousepad"],
["mouse","mousepad"]
]
<strong>Explanation:</strong> products sorted lexicographically = ["mobile","moneypot","monitor","mouse","mousepad"]
After typing m and mo all products match and we show user ["mobile","moneypot","monitor"]
After typing mou, mous and mouse the system suggests ["mouse","mousepad"]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> products = ["havana"], searchWord = "havana"
<strong>Output:</strong> [["havana"],["havana"],["havana"],["havana"],["havana"],["havana"]]
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> products = ["bags","baggage","banner","box","cloths"], searchWord = "bags"
<strong>Output:</strong> [["baggage","bags","banner"],["baggage","bags","banner"],["baggage","bags"],["bags"]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= products.length &lt;= 1000</code></li>
	<li><code>1 &lt;= products[i].length &lt;= 3000</code></li>
	<li><code>1 &lt;= sum(products[i].length) &lt;= 2 * 10<sup>4</sup></code></li>
	<li>All the strings of <code>products</code> are <strong>unique</strong>.</li>
	<li><code>products[i]</code> consists of lowercase English letters.</li>
	<li><code>1 &lt;= searchWord.length &lt;= 1000</code></li>
	<li><code>searchWord</code> consists of lowercase English letters.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Oracle](https://leetcode.com/company/oracle), [Apple](https://leetcode.com/company/apple), [Facebook](https://leetcode.com/company/facebook), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Trie](https://leetcode.com/tag/trie/)

## Solution 1. Trie + DFS

```py
# OJ: https://leetcode.com/problems/search-suggestions-system/
# Author: Duy
# Time: O(T*S) where T is the size of all the content in the `products`, S is the length of `searchWord`.
# Space: O(T) for the tree
# Ref: https://leetcode.com/problems/search-suggestions-system/discuss/1242823/C%2B%2BPython-3-solutions-Clean-and-Concise
class Trie:
    # Use Trie to keep track of prefix
    def __init__(self):
        self.word = None
        self.child = defaultdict(Trie)
    # Add a new word in to Trie
    def addWord(self, word):
        cur = self
        for c in word:
            # defauldict(Trie) helped to create a new Trie if empty
            cur = cur.child[c]
        cur.word = word
    def getWord(self, count):
        res = []
        def dfs(cur):
            if len(res) == count: return
            if cur.word != None:
                res.append(cur.word)
            # search into lexicographically order
            for c in ascii_lowercase:
                if c in cur.child:
                    dfs(cur.child[c])
        dfs(self)
        return res
class Solution:
    def suggestedProducts(self, products: List[str], searchWord: str) -> List[List[str]]:
        root = Trie()
        for p in products:
            root.addWord(p)
        res = list()
        cur = root
        for c in searchWord:
            if cur and c in cur.child:
                cur = cur.child[c]
                res.append(cur.getWord(3))
            else:
                # if cannot find any word, stop the search and return empty
                cur = None
                res.append([])
        return res
```

## Solution 2. Sort and Filter

```py
# OJ: https://leetcode.com/problems/search-suggestions-system/
# Author: Duy
# Time: O(M*N), N is number of products, M is length of searchWord
# Space: O(N)
class Solution:
    def suggestedProducts(self, products: List[str], searchWord: str) -> List[List[str]]:
        res = list()
        products.sort()
        # This for loop cost O(M * N)
        for i, c in enumerate(searchWord):
            r = list()
            # Find all p that has the same c
            for p in products:
                if i < len(p) and c == p[i]:
                    r.append(p)
            # Only take first 3 answer
            res.append(r[:3])
            # Update our products
            # Save time for next search
            products = r
        return res
```
