# [1423. Maximum Points You Can Obtain from Cards (Medium)](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)

<p>There are several cards <strong>arranged in a row</strong>, and each card has an associated number of points. The points are given in the integer array <code>cardPoints</code>.</p>

<p>In one step, you can take one card from the beginning or from the end of the row. You have to take exactly <code>k</code> cards.</p>

<p>Your score is the sum of the points of the cards you have taken.</p>

<p>Given the integer array <code>cardPoints</code> and the integer <code>k</code>, return the <em>maximum score</em> you can obtain.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> cardPoints = [1,2,3,4,5,6,1], k = 3
<strong>Output:</strong> 12
<strong>Explanation:</strong> After the first step, your score will always be 1. However, choosing the rightmost card first will maximize your total score. The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> cardPoints = [2,2,2], k = 2
<strong>Output:</strong> 4
<strong>Explanation:</strong> Regardless of which two cards you take, your score will always be 4.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> cardPoints = [9,7,7,9,7,7,9], k = 7
<strong>Output:</strong> 55
<strong>Explanation:</strong> You have to take all the cards. Your score is the sum of points of all cards.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= cardPoints.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= cardPoints[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= k &lt;= cardPoints.length</code></li>
</ul>

**Companies**:  
[Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Sliding Window](https://leetcode.com/tag/sliding-window/), [Prefix Sum](https://leetcode.com/tag/prefix-sum/)

**Similar Questions**:

- [Maximum Score from Performing Multiplication Operations (Medium)](https://leetcode.com/problems/maximum-score-from-performing-multiplication-operations/)
- [Removing Minimum and Maximum From Array (Medium)](https://leetcode.com/problems/removing-minimum-and-maximum-from-array/)

## Solution 1. Sliding Window

Let say we have `arr = [1, 2, 3, 4, 5, 6, 1]` and `k = 3`

Initially, our window is `1, 2, 3, 4` and `total = 5 + 6 + 1 = 12`

Then we move our window to the right by 1

Then our `total += arr[lo] - arr[hi]`, we add the left one and subtract the right one

We do this until the end of the array

We only move at K steps

```py
# OJ: https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/
# Author: Duy Tran
# Time: O(K)
# Space: O(1)

class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        lo, hi = 0, n - k
        total = sum(cardPoints[hi:]) #this cost O(K)
        res = total
        while hi < n:
            total += (cardPoints[lo] - cardPoints[hi])
            res = max(res, total)
            lo += 1
            hi += 1
        return res

```
