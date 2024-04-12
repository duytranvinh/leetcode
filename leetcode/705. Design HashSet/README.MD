# [705. Design HashSet (Easy)](https://leetcode.com/problems/design-hashset)

<p>Design a HashSet without using any built-in hash table libraries.</p>

<p>Implement <code>MyHashSet</code> class:</p>

<ul>
	<li><code>void add(key)</code> Inserts the value <code>key</code> into the HashSet.</li>
	<li><code>bool contains(key)</code> Returns whether the value <code>key</code> exists in the HashSet or not.</li>
	<li><code>void remove(key)</code> Removes the value <code>key</code> in the HashSet. If <code>key</code> does not exist in the HashSet, do nothing.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;MyHashSet&quot;, &quot;add&quot;, &quot;add&quot;, &quot;contains&quot;, &quot;contains&quot;, &quot;add&quot;, &quot;contains&quot;, &quot;remove&quot;, &quot;contains&quot;]
[[], [1], [2], [1], [3], [2], [2], [2], [2]]
<strong>Output</strong>
[null, null, null, true, false, null, true, null, false]

<strong>Explanation</strong>
MyHashSet myHashSet = new MyHashSet();
myHashSet.add(1);      // set = [1]
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(1); // return True
myHashSet.contains(3); // return False, (not found)
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(2); // return True
myHashSet.remove(2);   // set = [1]
myHashSet.contains(2); // return False, (already removed)</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= key &lt;= 10<sup>6</sup></code></li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to <code>add</code>, <code>remove</code>, and <code>contains</code>.</li>
</ul>

**Companies**:
[Apple](https://leetcode.com/company/apple), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Wix](https://leetcode.com/company/wix)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [Linked List](https://leetcode.com/tag/linked-list), [Design](https://leetcode.com/tag/design), [Hash Function](https://leetcode.com/tag/hash-function)

**Similar Questions**:

- [Design HashMap (Easy)](https://leetcode.com/problems/design-hashmap)
- [Design Skiplist (Hard)](https://leetcode.com/problems/design-skiplist)

## Solution 1.

Not the most optimal solution, but it solve the problem

Each method cost O(N) in Time Complexity

```py
# OJ: https://leetcode.com/problems/design-hashset
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class MyHashSet:
    def __init__(self):
      self.hashset = []

    def add(self, key: int) -> None:
      if not self.contains(key):
        self.hashset.append(key)

    def remove(self, key: int) -> None:
      if self.contains(key):
        self.hashset.remove(key)

    def contains(self, key: int) -> bool:
      return True if key in self.hashset else False

```

## Solution 2. Linked List with Bucket

A little bit faster with LinkedList

Create a hash key with mode function

There is only at most 10^4 calls will be made

![](https://leetcode.com/problems/design-hashset/Figures/705/705_linked_list.png)

```py
# OJ: https://leetcode.com/problems/design-hashset
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class ListNode:
  def __init__(self, key):
    self.key = key
    self.next = None

class MyHashSet:
    def __init__(self):
      # At most 10^4 calls will be made
      self.set = [ListNode(0) for i in range(10**4)]

    def _getHash(self, key):
      return key % len(self.set)

    def add(self, key: int) -> None:
      cur = self.set[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          return
        cur = cur.next
      cur.next = ListNode(key)

    def remove(self, key: int) -> None:
      cur = self.set[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          cur.next = cur.next.next
          return
        cur = cur.next

    def contains(self, key: int) -> bool:
      cur = self.set[self._getHash(key)]
      while cur.next:
        if cur.next.key == key:
          return True
```
