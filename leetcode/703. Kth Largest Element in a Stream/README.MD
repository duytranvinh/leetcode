# [703. Kth Largest Element in a Stream (Easy)](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

<p>Design a class to find the <code>k<sup>th</sup></code> largest element in a stream. Note that it is the <code>k<sup>th</sup></code> largest element in the sorted order, not the <code>k<sup>th</sup></code> distinct element.</p>

<p>Implement <code>KthLargest</code> class:</p>

<ul>
	<li><code>KthLargest(int k, int[] nums)</code> Initializes the object with the integer <code>k</code> and the stream of integers <code>nums</code>.</li>
	<li><code>int add(int val)</code> Appends the integer <code>val</code> to the stream and returns the element representing the <code>k<sup>th</sup></code> largest element in the stream.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
<strong>Output</strong>
[null, 4, 5, 5, 8, 8]

<strong>Explanation</strong>
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= val &lt;= 10<sup>4</sup></code></li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to <code>add</code>.</li>
	<li>It is guaranteed that there will be at least <code>k</code> elements in the array when you search for the <code>k<sup>th</sup></code> element.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe), [Amazon](https://leetcode.com/company/amazon), [LinkedIn](https://leetcode.com/company/linkedin), [Microsoft](https://leetcode.com/company/microsoft)

**Related Topics**:  
[Tree](https://leetcode.com/tag/tree/), [Design](https://leetcode.com/tag/design/), [Binary Search Tree](https://leetcode.com/tag/binary-search-tree/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Binary Tree](https://leetcode.com/tag/binary-tree/), [Data Stream](https://leetcode.com/tag/data-stream/)

**Similar Questions**:

- [Kth Largest Element in an Array (Medium)](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- [Finding MK Average (Hard)](https://leetcode.com/problems/finding-mk-average/)
- [Sequentially Ordinal Rank Tracker (Hard)](https://leetcode.com/problems/sequentially-ordinal-rank-tracker/)

## Solution 1.

`heapq` will keep the `heap` from smallest to largest in `k` size

```py
# OJ: https://leetcode.com/problems/kth-largest-element-in-a-stream/
# Author: Duy Tran
# Time: O(N), O(1)
# Space: O(N)

class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        # minHeap w/ K largest integers
        self.minHeap, self.k = nums, k
        heapq.heapify(self.minHeap)
        while len(self.minHeap) > k:
            heapq.heappop(self.minHeap)

    def add(self, val: int) -> int:
        heapq.heappush(self.minHeap, val)
        if len(self.minHeap) > self.k:
            heapq.heappop(self.minHeap)
        # print(self.minHeap)
        return self.minHeap[0]

# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)

```
