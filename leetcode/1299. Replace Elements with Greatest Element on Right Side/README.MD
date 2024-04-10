# [1299. Replace Elements with Greatest Element on Right Side (Easy)](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side)

<p>Given an array <code>arr</code>,&nbsp;replace every element in that array with the greatest element among the elements to its&nbsp;right, and replace the last element with <code>-1</code>.</p>

<p>After doing so, return the array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [17,18,5,4,6,1]
<strong>Output:</strong> [18,6,6,6,1,-1]
<strong>Explanation:</strong> 
- index 0 --&gt; the greatest element to the right of index 0 is index 1 (18).
- index 1 --&gt; the greatest element to the right of index 1 is index 4 (6).
- index 2 --&gt; the greatest element to the right of index 2 is index 4 (6).
- index 3 --&gt; the greatest element to the right of index 3 is index 4 (6).
- index 4 --&gt; the greatest element to the right of index 4 is index 5 (1).
- index 5 --&gt; there are no elements to the right of index 5, so we put -1.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [400]
<strong>Output:</strong> [-1]
<strong>Explanation:</strong> There are no elements to the right of index 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= arr[i] &lt;= 10<sup>5</sup></code></li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Adobe](https://leetcode.com/company/adobe), [Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Array](https://leetcode.com/tag/array)

**Similar Questions**:

- [Two Furthest Houses With Different Colors (Easy)](https://leetcode.com/problems/two-furthest-houses-with-different-colors)
- [Next Greater Element IV (Hard)](https://leetcode.com/problems/next-greater-element-iv)

**Hints**:

- Loop through the array starting from the end.
- Keep the maximum value seen so far.

## Solution 1.

Run from right to left, fill up best max

```py
# OJ: https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class  Solution:
        def  replaceElements(self,  arr:  List[int])  ->  List[int]:
                rightMax  =  -1
                for  i  in  range(len(arr)  -  1,  -1,  -1):
                    newMax  =  max(rightMax,  arr[i])
                    arr[i]  =  rightMax
                    rightMax  =  newMax
                return  arr

```
