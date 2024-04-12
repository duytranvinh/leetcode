# [706. Design HashMap (Easy)](https://leetcode.com/problems/design-hashmap)

<p>Design a HashMap without using any built-in hash table libraries.</p>

<p>Implement the <code>MyHashMap</code> class:</p>

<ul>
	<li><code>MyHashMap()</code> initializes the object with an empty map.</li>
	<li><code>void put(int key, int value)</code> inserts a <code>(key, value)</code> pair into the HashMap. If the <code>key</code> already exists in the map, update the corresponding <code>value</code>.</li>
	<li><code>int get(int key)</code> returns the <code>value</code> to which the specified <code>key</code> is mapped, or <code>-1</code> if this map contains no mapping for the <code>key</code>.</li>
	<li><code>void remove(key)</code> removes the <code>key</code> and its corresponding <code>value</code> if the map contains the mapping for the <code>key</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;MyHashMap&quot;, &quot;put&quot;, &quot;put&quot;, &quot;get&quot;, &quot;get&quot;, &quot;put&quot;, &quot;get&quot;, &quot;remove&quot;, &quot;get&quot;]
[[], [1, 1], [2, 2], [1], [3], [2, 1], [2], [2], [2]]
<strong>Output</strong>
[null, null, null, 1, -1, null, 1, null, -1]

<strong>Explanation</strong>
MyHashMap myHashMap = new MyHashMap();
myHashMap.put(1, 1); // The map is now [[1,1]]
myHashMap.put(2, 2); // The map is now [[1,1], [2,2]]
myHashMap.get(1);    // return 1, The map is now [[1,1], [2,2]]
myHashMap.get(3);    // return -1 (i.e., not found), The map is now [[1,1], [2,2]]
myHashMap.put(2, 1); // The map is now [[1,1], [2,1]] (i.e., update the existing value)
myHashMap.get(2);    // return 1, The map is now [[1,1], [2,1]]
myHashMap.remove(2); // remove the mapping for 2, The map is now [[1,1]]
myHashMap.get(2);    // return -1 (i.e., not found), The map is now [[1,1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= key, value &lt;= 10<sup>6</sup></code></li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to <code>put</code>, <code>get</code>, and <code>remove</code>.</li>
</ul>

**Companies**:
[Microsoft](https://leetcode.com/company/microsoft), [Amazon](https://leetcode.com/company/amazon), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [ServiceNow](https://leetcode.com/company/servicenow), [Apple](https://leetcode.com/company/apple), [Facebook](https://leetcode.com/company/facebook), [Two Sigma](https://leetcode.com/company/two-sigma), [Shopee](https://leetcode.com/company/shopee), [VMware](https://leetcode.com/company/vmware), [Walmart Labs](https://leetcode.com/company/walmart-labs), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [Linked List](https://leetcode.com/tag/linked-list), [Design](https://leetcode.com/tag/design), [Hash Function](https://leetcode.com/tag/hash-function)

**Similar Questions**:

- [Design HashSet (Easy)](https://leetcode.com/problems/design-hashset)
- [Design Skiplist (Hard)](https://leetcode.com/problems/design-skiplist)

## Solution 1.

Use LinkedList

Create a hash key with mode function

There is only at most 10^4 calls will be made

The bigger the number of bucket, the faster it is

![](https://leetcode.com/problems/design-hashmap/Figures/706/706_hashmap.png)

```py
# OJ: https://leetcode.com/problems/design-hashmap
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class ListNode:
  def __init__(self, key = -1, value = -1, next = None):
    self.key = key
    self.value =  value
    self.next = next

class MyHashMap:

    def __init__(self):
      # At most 10^4 calls will be made
      self.map = [ListNode() for i in range(10**4)]

    def _getHash(self, key):
      return key % len(self.map)

    def put(self, key: int, value: int) -> None:
      cur = self.map[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          cur.next.value = value
          return
        cur = cur.next
      cur.next = ListNode(key, value)

    def get(self, key: int) -> int:
      cur = self.map[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          return cur.next.value
        cur = cur.next
      return -1

    def remove(self, key: int) -> None:
      cur = self.map[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          cur.next =  cur.next.next
          return
        cur = cur.next

# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)

```
