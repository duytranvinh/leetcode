# [239. Sliding Window Maximum (Hard)](https://leetcode.com/problems/sliding-window-maximum/)

<p>You are given an array of integers&nbsp;<code>nums</code>, there is a sliding window of size <code>k</code> which is moving from the very left of the array to the very right. You can only see the <code>k</code> numbers in the window. Each time the sliding window moves right by one position.</p>

<p>Return <em>the max sliding window</em>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,3,-1,-3,5,3,6,7], k = 3
<strong>Output:</strong> [3,3,5,5,6,7]
<strong>Explanation:</strong> 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       <strong>3</strong>
 1 [3  -1  -3] 5  3  6  7       <strong>3</strong>
 1  3 [-1  -3  5] 3  6  7      <strong> 5</strong>
 1  3  -1 [-3  5  3] 6  7       <strong>5</strong>
 1  3  -1  -3 [5  3  6] 7       <strong>6</strong>
 1  3  -1  -3  5 [3  6  7]      <strong>7</strong>
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= k &lt;= nums.length</code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Google](https://leetcode.com/company/google), [Microsoft](https://leetcode.com/company/microsoft), [Uber](https://leetcode.com/company/uber), [Salesforce](https://leetcode.com/company/salesforce), [Facebook](https://leetcode.com/company/facebook), [Apple](https://leetcode.com/company/apple), [Citadel](https://leetcode.com/company/citadel), [ByteDance](https://leetcode.com/company/bytedance), [Bloomberg](https://leetcode.com/company/bloomberg), [Adobe](https://leetcode.com/company/adobe), [Twilio](https://leetcode.com/company/twilio), [tiktok](https://leetcode.com/company/tiktok), [VMware](https://leetcode.com/company/vmware), [Booking.com](https://leetcode.com/company/bookingcom), [Quora](https://leetcode.com/company/quora), [Cruise Automation](https://leetcode.com/company/cruise-automation)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Queue](https://leetcode.com/tag/queue/), [Sliding Window](https://leetcode.com/tag/sliding-window/), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue/), [Monotonic Queue](https://leetcode.com/tag/monotonic-queue/)

**Similar Questions**:

- [Minimum Window Substring (Hard)](https://leetcode.com/problems/minimum-window-substring/)
- [Min Stack (Easy)](https://leetcode.com/problems/min-stack/)
- [Longest Substring with At Most Two Distinct Characters (Medium)](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
- [Paint House II (Hard)](https://leetcode.com/problems/paint-house-ii/)
- [Jump Game VI (Medium)](https://leetcode.com/problems/jump-game-vi/)

## Solution 1. Sliding Window

Assume the array is `[3, 1, 2, ...]` and `k = 3`, popping `3` out of the window will result in max value update, but popping `1` won't. This means that we can just keep track of `[3, 2]`, i.e. a monotonically decreasing sequence of values.

Here we store the `index` of the monotonically decreasing sequence. When a new value `A[i]` is added to the window, we pop the trailing `index` in the dequeue which are pointing to values that are smaller or equal to `A[i]`. Then we can push i into the dequeue.

We need to pop the index which falls out of the window from the dequeue as well.

```py
# OJ: https://leetcode.com/problems/sliding-window-maximum/
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res = list()
        q = collections.deque() #store index
        l, r = 0, 0
        while r < len(nums):
            #popping right, to make the dequeue decreasing
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)

            # if left is out of the window, popleft
            if l > q[0]:
                q.popleft()

            # when the window is established, we shrink left
            if (r + 1) >= k:
                res.append(nums[q[0]])
                l += 1
            r += 1
        return res
```
