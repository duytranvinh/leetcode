# [605. Can Place Flowers (Easy)](https://leetcode.com/problems/can-place-flowers)

<p>You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in <strong>adjacent</strong> plots.</p>

<p>Given an integer array <code>flowerbed</code> containing <code>0</code>&#39;s and <code>1</code>&#39;s, where <code>0</code> means empty and <code>1</code> means not empty, and an integer <code>n</code>, return <code>true</code>&nbsp;<em>if</em> <code>n</code> <em>new flowers can be planted in the</em> <code>flowerbed</code> <em>without violating the no-adjacent-flowers rule and</em> <code>false</code> <em>otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 1
<strong>Output:</strong> true
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 2
<strong>Output:</strong> false
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= flowerbed.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>flowerbed[i]</code> is <code>0</code> or <code>1</code>.</li>
	<li>There are no two adjacent flowers in <code>flowerbed</code>.</li>
	<li><code>0 &lt;= n &lt;= flowerbed.length</code></li>
</ul>

**Companies**:
[Facebook](https://leetcode.com/company/facebook), [LinkedIn](https://leetcode.com/company/linkedin), [Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Microsoft](https://leetcode.com/company/microsoft), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Greedy](https://leetcode.com/tag/greedy)

**Similar Questions**:

- [Teemo Attacking (Easy)](https://leetcode.com/problems/teemo-attacking)
- [Asteroid Collision (Medium)](https://leetcode.com/problems/asteroid-collision)

## Solution 1.

If the spot is empty, then check prev and next to see if it empty too

There are two edge case here:

- At first spot `i = 0`, then we just need to check the current & next spot

- At last spot `i = n-1`, then we just need to check the current & prev spot

```py
# OJ: https://leetcode.com/problems/can-place-flowers
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def canPlaceFlowers(self, arr: List[int], n: int) -> bool:
      for i in range(len(arr)):
        if n == 0: return True
        if (i == 0 or arr[i - 1] == 0) and arr[i] == 0 and (i == (len(arr) - 1) or arr[i + 1] == 0):
          arr[i] = 1
          n -=1
      return n == 0

```
