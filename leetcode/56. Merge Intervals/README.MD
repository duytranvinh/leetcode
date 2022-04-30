# [56. Merge Intervals (Medium)](https://leetcode.com/problems/merge-intervals/)

<p>Given an array&nbsp;of <code>intervals</code>&nbsp;where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return <em>an array of the non-overlapping intervals that cover all the intervals in the input</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,3],[2,6],[8,10],[15,18]]
<strong>Output:</strong> [[1,6],[8,10],[15,18]]
<strong>Explanation:</strong> Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,4],[4,5]]
<strong>Output:</strong> [[1,5]]
<strong>Explanation:</strong> Intervals [1,4] and [4,5] are considered overlapping.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= intervals.length &lt;= 10<sup>4</sup></code></li>
	<li><code>intervals[i].length == 2</code></li>
	<li><code>0 &lt;= start<sub>i</sub> &lt;= end<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [Salesforce](https://leetcode.com/company/salesforce), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Uber](https://leetcode.com/company/uber), [Adobe](https://leetcode.com/company/adobe), [LinkedIn](https://leetcode.com/company/linkedin), [IBM](https://leetcode.com/company/ibm), [VMware](https://leetcode.com/company/vmware), [Snapchat](https://leetcode.com/company/snapchat), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [Oracle](https://leetcode.com/company/oracle), [Yandex](https://leetcode.com/company/yandex), [tiktok](https://leetcode.com/company/tiktok), [Shopee](https://leetcode.com/company/shopee), [Twitter](https://leetcode.com/company/twitter), [ByteDance](https://leetcode.com/company/bytedance)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Sorting](https://leetcode.com/tag/sorting/)

**Similar Questions**:

- [Insert Interval (Medium)](https://leetcode.com/problems/insert-interval/)
- [Meeting Rooms (Easy)](https://leetcode.com/problems/meeting-rooms/)
- [Meeting Rooms II (Medium)](https://leetcode.com/problems/meeting-rooms-ii/)
- [Teemo Attacking (Easy)](https://leetcode.com/problems/teemo-attacking/)
- [Add Bold Tag in String (Medium)](https://leetcode.com/problems/add-bold-tag-in-string/)
- [Range Module (Hard)](https://leetcode.com/problems/range-module/)
- [Employee Free Time (Hard)](https://leetcode.com/problems/employee-free-time/)
- [Partition Labels (Medium)](https://leetcode.com/problems/partition-labels/)
- [Interval List Intersections (Medium)](https://leetcode.com/problems/interval-list-intersections/)
- [Amount of New Area Painted Each Day (Hard)](https://leetcode.com/problems/amount-of-new-area-painted-each-day/)
- [Longest Substring of One Repeating Character (Hard)](https://leetcode.com/problems/longest-substring-of-one-repeating-character/)

## Solution 1.

```PY
# OJ: https://leetcode.com/problems/merge-intervals/
# Author: Duy Tran
# Time: O(N logN)
# Space: O(N)

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        #sort by first key
        intervals.sort(key = lambda x: x[0])
        print(intervals)
        res = list()
        for interval in intervals:
            # if the list of merged intervals is empty
            if not res:
                res.append(interval)
                continue
            # if the current interval does not overlap
            # with the previous, simply append it.
            if res[-1][1] < interval[0]:
                res.append(interval)
            else:
                res[-1][1] = max(res[-1][1], interval[1])
        return res

```
