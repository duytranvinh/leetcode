# [1094. Car Pooling (Medium)](https://leetcode.com/problems/car-pooling/)

<p>There is a car with <code>capacity</code> empty seats. The vehicle only drives east (i.e., it cannot turn around and drive west).</p>

<p>You are given the integer <code>capacity</code> and an array <code>trips</code> where <code>trips[i] = [numPassengers<sub>i</sub>, from<sub>i</sub>, to<sub>i</sub>]</code> indicates that the <code>i<sup>th</sup></code> trip has <code>numPassengers<sub>i</sub></code> passengers and the locations to pick them up and drop them off are <code>from<sub>i</sub></code> and <code>to<sub>i</sub></code> respectively. The locations are given as the number of kilometers due east from the car's initial location.</p>

<p>Return <code>true</code><em> if it is possible to pick up and drop off all passengers for all the given trips, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> trips = [[2,1,5],[3,3,7]], capacity = 4
<strong>Output:</strong> false
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> trips = [[2,1,5],[3,3,7]], capacity = 5
<strong>Output:</strong> true
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= trips.length &lt;= 1000</code></li>
	<li><code>trips[i].length == 3</code></li>
	<li><code>1 &lt;= numPassengers<sub>i</sub> &lt;= 100</code></li>
	<li><code>0 &lt;= from<sub>i</sub> &lt; to<sub>i</sub> &lt;= 1000</code></li>
	<li><code>1 &lt;= capacity &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [DoorDash](https://leetcode.com/company/doordash), [Flipkart](https://leetcode.com/company/flipkart), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Bloomberg](https://leetcode.com/company/bloomberg), [Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Sorting](https://leetcode.com/tag/sorting/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Simulation](https://leetcode.com/tag/simulation/), [Prefix Sum](https://leetcode.com/tag/prefix-sum/)

**Similar Questions**:

- [Meeting Rooms II (Medium)](https://leetcode.com/problems/meeting-rooms-ii/)

## Solution 1. Heap

```py
# OJ: https://leetcode.com/problems/car-pooling/
# Author: Duy Tran
# Time: O(N logN)
# Space: O(N)

class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        trips.sort(key = lambda x: x[1])
        minHeap = [] # [end, numPassengers]
        curPass = 0
        for t in trips:
            numPass, start, end = t
            #Dropping of passengers
            while minHeap and minHeap[0][0] <= start:
                curPass -= minHeap[0][1]
                heapq.heappop(minHeap)
            curPass += numPass
            if curPass > capacity:
                return False
            heapq.heappush(minHeap, [end, numPass])
        return True

```

## Solution 2. Bucket sort

```py
# OJ: https://leetcode.com/problems/car-pooling/
# Author: Duy Tran
# Time: O(N, 1001)
# Space: O(1), 1001 for bucket size

class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # Base on the constraints
        # 1 <= trips.length <= 1000
        # Therefore, we can use bucket sort
        bucket = [0 for _ in range(1001)]
        #Fill the bucket
        for t in trips:
            numPass, start, end = t
            bucket[start] += numPass
            bucket[end] -= numPass
        #Check the bucket
        curPass = 0
        for i in range(1001):
            curPass += bucket[i]
            if curPass > capacity:
                return False
        return True
```

## Solution 3. Bucket sort but with dict

```py
# OJ: https://leetcode.com/problems/car-pooling/
# Author: Duy Tran
# Time: O(N)
# Space: O(S + E), the size of bucket depend on the unique number of time
# Same as Solution 2, but use SortedDict
# Therefore, we don't need to care about the constraint

from sortedcontainers import SortedDict
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        bucket = SortedDict()
        for t in trips:
            numPass, start, end = t
            bucket[start] = bucket.get(start, 0) + numPass
            bucket[end] = bucket.get(end, 0) - numPass
        print(bucket)
        #Check the bucket
        curPass = 0
        for time in bucket:
            curPass += bucket[time]
            if curPass > capacity:
                return False
        return True
```

## Solution 4. Two sorted array

```py
# OJ: https://leetcode.com/problems/car-pooling/
# Author: Duy Tran
# Time: O(N logN)
# Space: O(N)

class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # whenever you pass a pickup point, you have to pick up the passengers
        #   if passengers exceeds capacity, return false
        # whenever you pass a dropoff point, you drop off the passengers
        pickups = sorted([(x[1], x[0]) for x in trips])
        dropoffs = sorted([(x[2], x[0]) for x in trips])
        i, j = 0,0
        passengers = 0
        while i < len(trips):
            if dropoffs[j][0] <= pickups[i][0]:
                passengers -= dropoffs[j][1]
                j += 1
            else:
                passengers += pickups[i][1]
                if passengers > capacity:
                    return False
                i += 1
        return True
```
