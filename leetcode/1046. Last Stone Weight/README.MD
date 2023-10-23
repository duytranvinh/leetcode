# [1046. Last Stone Weight (Easy)](https://leetcode.com/problems/last-stone-weight)

<p>You are given an array of integers <code>stones</code> where <code>stones[i]</code> is the weight of the <code>i<sup>th</sup></code> stone.</p>

<p>We are playing a game with the stones. On each turn, we choose the <strong>heaviest two stones</strong> and smash them together. Suppose the heaviest two stones have weights <code>x</code> and <code>y</code> with <code>x &lt;= y</code>. The result of this smash is:</p>

<ul>
	<li>If <code>x == y</code>, both stones are destroyed, and</li>
	<li>If <code>x != y</code>, the stone of weight <code>x</code> is destroyed, and the stone of weight <code>y</code> has new weight <code>y - x</code>.</li>
</ul>

<p>At the end of the game, there is <strong>at most one</strong> stone left.</p>

<p>Return <em>the weight of the last remaining stone</em>. If there are no stones left, return <code>0</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> stones = [2,7,4,1,8,1]
<strong>Output:</strong> 1
<strong>Explanation:</strong> 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that&#39;s the value of the last stone.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> stones = [1]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= stones.length &lt;= 30</code></li>
	<li><code>1 &lt;= stones[i] &lt;= 1000</code></li>
</ul>


**Companies**:
[Nvidia](https://leetcode.com/company/nvidia), [Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber), [Visa](https://leetcode.com/company/visa), [LinkedIn](https://leetcode.com/company/linkedin), [VMware](https://leetcode.com/company/vmware), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe), [Salesforce](https://leetcode.com/company/salesforce), [Apple](https://leetcode.com/company/apple), [Grammarly](https://leetcode.com/company/grammarly)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue)

**Hints**:
* Simulate the process.  We can do it with a heap, or by sorting some list of stones every time we take a turn.

## Solutions

1. Array-Based Simulation

    - Find the two largest stone and keep removing them out (or add them into the back)

    - Time: O(N^2)

    - Space: O(N) or swapping to get O(1)

2. Sorted Array-Based Simulation

    - Sort array and get the largest stones out one by one

    - Time: O(N^2), sort is O(NlogN) but when we loop through stones O(N) and re-insert (which cost O(N))
    
    - Space: O(N)

3. Heap-Based Simulation

    - Heap to get sorted, and then removing it one by one

    - Time: O(NlogN)

    - Space: O(N)

    - Best optimal, but not supported in Javascript

### Solution 3. Heap

Pseudocode 

```
define function last_stone_weight(stones):
    heap = a new Max-Heap
    add all stones to heap
    while heap contains more than 1 stone:
        heavy_stone_1 = remove max from heap
        heavy_stone_2 = remove max from heap
        if heavy_stone_1 is heavier than heavy_stone_2:
            new_stone = heavy_stone_1 - heavy_stone_2
            add new_stone to heap
    if heap is empty:
        return 0
    return last stone on heap
```
#### Python

```py
# OJ: https://leetcode.com/problems/last-stone-weight
# Author: Duy Tran
# Time: O(NlogN)
# Space: O(N)

class Solution:
  def lastStoneWeight(self, stones: List[int]) -> int:
    stones = [-s for s in stones]
    heapq.heapify(stones)
    while (len(stones) > 1):
        first = abs(heapq.heappop(stones))
        second = abs(heapq.heappop(stones))
        if first > second:
            heapq.heappush(stones, -(first - second))
    if len(stones) > 0:
        return abs(heapq.heappop(stones))
    return 0
```

short hand version

```py
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        h = [-x for x in stones]
        heapq.heapify(h)
        while len(h) > 1 and h[0] != 0:
            heapq.heappush(h, heapq.heappop(h) - heapq.heappop(h))
        return -h[0]
```