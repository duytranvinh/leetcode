# [146. LRU Cache (Medium)](https://leetcode.com/problems/lru-cache/)

<p>Design a data structure that follows the constraints of a <strong><a href="https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU" target="_blank">Least Recently Used (LRU) cache</a></strong>.</p>

<p>Implement the <code>LRUCache</code> class:</p>

<ul>
	<li><code>LRUCache(int capacity)</code> Initialize the LRU cache with <strong>positive</strong> size <code>capacity</code>.</li>
	<li><code>int get(int key)</code> Return the value of the <code>key</code> if the key exists, otherwise return <code>-1</code>.</li>
	<li><code>void put(int key, int value)</code>&nbsp;Update the value of the <code>key</code> if the <code>key</code> exists. Otherwise, add the <code>key-value</code> pair to the cache. If the number of keys exceeds the <code>capacity</code> from this operation, <strong>evict</strong> the least recently used key.</li>
</ul>

<p>The functions&nbsp;<code data-stringify-type="code">get</code>&nbsp;and&nbsp;<code data-stringify-type="code">put</code>&nbsp;must each run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
<strong>Output</strong>
[null, null, null, 1, null, -1, null, -1, 3, 4]

<strong>Explanation</strong>
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= capacity &lt;= 3000</code></li>
	<li><code>0 &lt;= key &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>5</sup></code></li>
	<li>At most 2<code>&nbsp;* 10<sup>5</sup></code>&nbsp;calls will be made to <code>get</code> and <code>put</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Apple](https://leetcode.com/company/apple), [Oracle](https://leetcode.com/company/oracle), [Salesforce](https://leetcode.com/company/salesforce), [Twilio](https://leetcode.com/company/twilio), [Google](https://leetcode.com/company/google), [Intuit](https://leetcode.com/company/intuit), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [tiktok](https://leetcode.com/company/tiktok), [Adobe](https://leetcode.com/company/adobe), [LinkedIn](https://leetcode.com/company/linkedin), [Yahoo](https://leetcode.com/company/yahoo), [Snapchat](https://leetcode.com/company/snapchat), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [ByteDance](https://leetcode.com/company/bytedance), [Nvidia](https://leetcode.com/company/nvidia), [Shopee](https://leetcode.com/company/shopee)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [Linked List](https://leetcode.com/tag/linked-list/), [Design](https://leetcode.com/tag/design/), [Doubly-Linked List](https://leetcode.com/tag/doubly-linked-list/)

**Similar Questions**:

- [LFU Cache (Hard)](https://leetcode.com/problems/lfu-cache/)
- [Design In-Memory File System (Hard)](https://leetcode.com/problems/design-in-memory-file-system/)
- [Design Compressed String Iterator (Easy)](https://leetcode.com/problems/design-compressed-string-iterator/)
- [Design Most Recently Used Queue (Medium)](https://leetcode.com/problems/design-most-recently-used-queue/)

## Solution 1. Double Linked List

```PY
# OJ: https://leetcode.com/problems/lru-cache/
# Author: Duy Tran
# Time: O(1)
# Space: O(1)

class Node:
    def __init__(self, k, v):
        self.key = k
        self.val = v
        self.prev = None
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        #dict with key: key, val: node
        self.capacity = capacity
        self.dic = dict()

        # Empty head and tail to avoid edge case
            # is node.prev null?
            # is node.next null?
            # does it change if # of nodes < 2?
            # does it change if # of nodes > 2?
        # Adding the dummy nodes removes these concerns
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head


    def get(self, key: int) -> int:
        # check if key in dict
        if key not in self.dic:
            return -1
        # remove the from DLL and add it back to "tail"
        n = self.dic[key]
        self._remove(n)
        self._add(n)
        return n.val


    def put(self, key: int, value: int) -> None:
        # if key in dict, remove it
        if key in self.dic:
            self._remove(self.dic[key])

        # add node to dict and DLL
        n = Node(key, value)
        self._add(n)
        self.dic[key] = n

        # if oversize, the remove the head (Least Recent Use)
        if len(self.dic) > self.capacity:
            n = self.head.next
            self._remove(n)
            del self.dic[n.key]


    def _remove(self, node):
        #connect prev to next, and opposite
        p = node.prev
        n = node.next
        p.next = n
        n.prev = p

    def _add(self, node):
        #get the last node p
        p = self.tail.prev

        #connect p to node
        p.next = node

        #connect tail.prev to node
        self.tail.prev = node

        #connect node to p and tail
        node.prev = p
        node.next = self.tail


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
