# [208. Implement Trie (Prefix Tree) (Medium)](https://leetcode.com/problems/implement-trie-prefix-tree/)

<p>A <a href="https://en.wikipedia.org/wiki/Trie" target="_blank"><strong>trie</strong></a> (pronounced as "try") or <strong>prefix tree</strong> is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.</p>

<p>Implement the Trie class:</p>

<ul>
	<li><code>Trie()</code> Initializes the trie object.</li>
	<li><code>void insert(String word)</code> Inserts the string <code>word</code> into the trie.</li>
	<li><code>boolean search(String word)</code> Returns <code>true</code> if the string <code>word</code> is in the trie (i.e., was inserted before), and <code>false</code> otherwise.</li>
	<li><code>boolean startsWith(String prefix)</code> Returns <code>true</code> if there is a previously inserted string <code>word</code> that has the prefix <code>prefix</code>, and <code>false</code> otherwise.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
<strong>Output</strong>
[null, null, true, false, true, null, true]

<strong>Explanation</strong>
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word.length, prefix.length &lt;= 2000</code></li>
	<li><code>word</code> and <code>prefix</code> consist only of lowercase English letters.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls <strong>in total</strong> will be made to <code>insert</code>, <code>search</code>, and <code>startsWith</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Twitter](https://leetcode.com/company/twitter), [Microsoft](https://leetcode.com/company/microsoft), [Snapchat](https://leetcode.com/company/snapchat), [Oracle](https://leetcode.com/company/oracle), [Apple](https://leetcode.com/company/apple), [Docusign](https://leetcode.com/company/docusign), [Facebook](https://leetcode.com/company/facebook), [ByteDance](https://leetcode.com/company/bytedance), [Opendoor](https://leetcode.com/company/opendoor)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [String](https://leetcode.com/tag/string/), [Design](https://leetcode.com/tag/design/), [Trie](https://leetcode.com/tag/trie/)

**Similar Questions**:

- [Design Add and Search Words Data Structure (Medium)](https://leetcode.com/problems/design-add-and-search-words-data-structure/)
- [Design Search Autocomplete System (Hard)](https://leetcode.com/problems/design-search-autocomplete-system/)
- [Replace Words (Medium)](https://leetcode.com/problems/replace-words/)
- [Implement Magic Dictionary (Medium)](https://leetcode.com/problems/implement-magic-dictionary/)
- [Encrypt and Decrypt Strings (Hard)](https://leetcode.com/problems/encrypt-and-decrypt-strings/)
- [Implement Trie II (Prefix Tree) (Medium)](https://leetcode.com/problems/implement-trie-ii-prefix-tree/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/implement-trie-prefix-tree/
# Author: Duy Tran
# Time: O()
# Space: O()

class TrieNode:
    def __init__(self):
        self.child = defaultdict(TrieNode)
        self.end = False

class Trie:

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        cur = self.root
        for c in word:
            # defauldict(Trie) helped to create a new Trie if empty
            cur = cur.child[c]
        cur.end = True

    def search(self, word: str) -> bool:
        cur = self.root
        for c in word:
            cur = cur.child.get(c)
            if cur is None:
                return False
        return cur.end

    def startsWith(self, prefix: str) -> bool:
        cur = self.root
        for c in prefix:
            cur = cur.child.get(c)
            if cur is None:
                return False
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)

```
