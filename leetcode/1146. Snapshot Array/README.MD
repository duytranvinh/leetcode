# [1146. Snapshot Array (Medium)](https://leetcode.com/problems/snapshot-array/)

<p>Implement a SnapshotArray that supports the following interface:</p>

<ul>
	<li><code>SnapshotArray(int length)</code> initializes an array-like data structure with the given length.&nbsp; <strong>Initially, each element equals 0</strong>.</li>
	<li><code>void set(index, val)</code> sets the element at the given <code>index</code> to be equal to <code>val</code>.</li>
	<li><code>int snap()</code>&nbsp;takes a snapshot of the array and returns the <code>snap_id</code>: the total number of times we called <code>snap()</code> minus <code>1</code>.</li>
	<li><code>int get(index, snap_id)</code>&nbsp;returns the value at the given <code>index</code>, at the time we took the snapshot with the given <code>snap_id</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> ["SnapshotArray","set","snap","set","get"]
[[3],[0,5],[],[0,6],[0,0]]
<strong>Output:</strong> [null,null,0,null,5]
<strong>Explanation: </strong>
SnapshotArray snapshotArr = new SnapshotArray(3); // set the length to be 3
snapshotArr.set(0,5);  // Set array[0] = 5
snapshotArr.snap();  // Take a snapshot, return snap_id = 0
snapshotArr.set(0,6);
snapshotArr.get(0,0);  // Get the value of array[0] with snap_id = 0, return 5</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= length&nbsp;&lt;= 50000</code></li>
	<li>At most <code>50000</code>&nbsp;calls will be made to <code>set</code>, <code>snap</code>, and <code>get</code>.</li>
	<li><code>0 &lt;= index&nbsp;&lt;&nbsp;length</code></li>
	<li><code>0 &lt;=&nbsp;snap_id &lt;&nbsp;</code>(the total number of times we call <code>snap()</code>)</li>
	<li><code>0 &lt;=&nbsp;val &lt;= 10^9</code></li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Rubrik](https://leetcode.com/company/rubrik), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Binary Search](https://leetcode.com/tag/binary-search/), [Design](https://leetcode.com/tag/design/)

## Solution 1.

Use array `snapshot` with `index = snap_id` and `value = hashmap`

`snapshot[i]` contains all the values changed between snapshot `i-1` and `i`

```py
# OJ: https://leetcode.com/problems/snapshot-array/
# Author: Duy Tran
# Time:
#     SnapshotArray, set, snap: O(1)
#     get: O(S) where S is the number of snapshots taken.
# Space: O(NS)

class SnapshotArray:
    def __init__(self, length: int):
        self.snapshot = [defaultdict(int)]

    def set(self, index: int, val: int) -> None:
        self.snapshot[-1][index] = val

    def snap(self) -> int:
        self.snapshot.append(defaultdict(int))
        return len(self.snapshot) - 2

    def get(self, index: int, snap_id: int) -> int:
        for i in range(snap_id, -1, -1):
            if index not in self.snapshot[i]: continue
            return self.snapshot[i][index]
        return 0

# Your SnapshotArray object will be instantiated and called as such:
# obj = SnapshotArray(length)
# obj.set(index,val)
# param_2 = obj.snap()
# param_3 = obj.get(index,snap_id)

```

## Solution 2.

Optimized base on solution 1

Use extra `snapIDs` arr to keep track which snapshots change the value of index

`snapIDs` will contain the array with `snapIDs[i] = []` with `i` is the index, and the array value contain the `snap_id` that capture changed

When we call `get()`, we will use `bisect.bisect_right()` to find the last changed `snap_id`

- Let says `snapIDs[index] = arr = [2, 5]`. Then `bisect.bisect_right(arr, 4)` will return `2`

- At `snapIDs[index][2 - 1]` contain the lasted-change-snap_id

- If we got `0`, which means that value at `index` never change. So we return default value `0`

- `bisect.bisect_right(arr, snap_id)` cost log(S) where S the number of snapshot we took that `index` aka the length of `arr`

```py
# OJ: https://leetcode.com/problems/snapshot-array/
# Author: Duy Tran
# SnapshotArray: O(N)
#      set: O(1)
#      snap: O(N)
#      get: O(logS) where S is the number of snapshots taken
# Space: O(NS)

import bisect
class SnapshotArray:
    def __init__(self, length: int):
        self.snapIDs = [[] for _ in range(length)]
        self.snapshot = [defaultdict(int)]

    def set(self, index: int, val: int) -> None:
        self.snapshot[-1][index] = val

    def snap(self) -> int:
        id = len(self.snapshot) - 1
        for index in self.snapshot[-1]:
            self.snapIDs[index].append(id)
        self.snapshot.append(defaultdict(int))
        return id

    def get(self, index: int, snap_id: int) -> int:
        listOfSnaps = self.snapIDs[index]
        i = bisect.bisect_right(listOfSnaps, snap_id) - 1
        return 0 if i == -1 else self.snapshot[listOfSnaps[i]][index]

# Your SnapshotArray object will be instantiated and called as such:
# obj = SnapshotArray(length)
# obj.set(index,val)
# param_2 = obj.snap()
# param_3 = obj.get(index,snap_id)
```
