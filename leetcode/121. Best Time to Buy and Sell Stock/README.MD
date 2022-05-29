# [121. Best Time to Buy and Sell Stock (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

<p>You are given an array <code>prices</code> where <code>prices[i]</code> is the price of a given stock on the <code>i<sup>th</sup></code> day.</p>

<p>You want to maximize your profit by choosing a <strong>single day</strong> to buy one stock and choosing a <strong>different day in the future</strong> to sell that stock.</p>

<p>Return <em>the maximum profit you can achieve from this transaction</em>. If you cannot achieve any profit, return <code>0</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> prices = [7,1,5,3,6,4]
<strong>Output:</strong> 5
<strong>Explanation:</strong> Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> prices = [7,6,4,3,1]
<strong>Output:</strong> 0
<strong>Explanation:</strong> In this case, no transactions are done and the max profit = 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= prices.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= prices[i] &lt;= 10<sup>4</sup></code></li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Microsoft](https://leetcode.com/company/microsoft), [Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Adobe](https://leetcode.com/company/adobe), [Apple](https://leetcode.com/company/apple), [Uber](https://leetcode.com/company/uber), [Oracle](https://leetcode.com/company/oracle), [Expedia](https://leetcode.com/company/expedia), [JPMorgan](https://leetcode.com/company/jpmorgan), [Capital One](https://leetcode.com/company/capital-one), [Paypal](https://leetcode.com/company/paypal), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [VMware](https://leetcode.com/company/vmware), [Cisco](https://leetcode.com/company/cisco), [Salesforce](https://leetcode.com/company/salesforce), [Atlassian](https://leetcode.com/company/atlassian), [Alation](https://leetcode.com/company/alation)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Dynamic Programming](https://leetcode.com/tag/dynamic-programming/)

**Similar Questions**:

- [Maximum Subarray (Easy)](https://leetcode.com/problems/maximum-subarray/)
- [Best Time to Buy and Sell Stock II (Medium)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)
- [Best Time to Buy and Sell Stock III (Hard)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)
- [Best Time to Buy and Sell Stock IV (Hard)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)
- [Best Time to Buy and Sell Stock with Cooldown (Medium)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
- [Sum of Beauty in the Array (Medium)](https://leetcode.com/problems/sum-of-beauty-in-the-array/)
- [Maximum Difference Between Increasing Elements (Easy)](https://leetcode.com/problems/maximum-difference-between-increasing-elements/)

## Solution 1. Sliding Window

Start with `lo = 0, hi = 1`

Then we keep sliding to the right until `price[lo] > price[hi]`, then we push the left side of our window to `lo = hi`

```py
# OJ: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        lo, hi = 0, 1
        res = 0
        while hi < len(prices):
            if prices[lo] < prices[hi]:
                profit = prices[hi] - prices[lo]
                res = max(res, profit)
            else:
                lo = hi
            hi += 1
        return  res

```
