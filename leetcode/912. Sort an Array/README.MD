# [912. Sort an Array (Medium)](https://leetcode.com/problems/sort-an-array)

<p>Given an array of integers <code>nums</code>, sort the array in ascending order and return it.</p>

<p>You must solve the problem <strong>without using any built-in</strong> functions in <code>O(nlog(n))</code> time complexity and with the smallest space complexity possible.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [5,2,3,1]
<strong>Output:</strong> [1,2,3,5]
<strong>Explanation:</strong> After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [5,1,1,2,0,0]
<strong>Output:</strong> [0,0,1,1,2,5]
<strong>Explanation:</strong> Note that the values of nums are not necessairly unique.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>-5 * 10<sup>4</sup> &lt;= nums[i] &lt;= 5 * 10<sup>4</sup></code></li>
</ul>

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Yahoo](https://leetcode.com/company/yahoo), [Apple](https://leetcode.com/company/apple), [Adobe](https://leetcode.com/company/adobe), [Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Uber](https://leetcode.com/company/uber), [Bloomberg](https://leetcode.com/company/bloomberg), [Facebook](https://leetcode.com/company/facebook)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer), [Sorting](https://leetcode.com/tag/sorting), [Heap (Priority Queue)](https://leetcode.com/tag/heap-priority-queue), [Merge Sort](https://leetcode.com/tag/merge-sort), [Bucket Sort](https://leetcode.com/tag/bucket-sort), [Radix Sort](https://leetcode.com/tag/radix-sort), [Counting Sort](https://leetcode.com/tag/counting-sort)

## Solutions

![](https://leetcode.com/problems/sort-an-array/Figures/912/Slide1.PNG)

## Solution 1. Merge Sort

```py
# OJ: https://leetcode.com/problems/sort-an-array
# Author: Duy Tran
# Time: O(NlogN)
# Space: O(N)


class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
      def merge(arr, l, m, r):
        left = arr[l: m + 1]
        right = arr[m + 1: r + 1]
        i, j, k = l, 0, 0
        while j < len(left) and k < len(right):
          if left[j] <= right[k]:
            arr[i] = left[j]
            j += 1
          else:
            arr[i] = right[k]
            k += 1
          i += 1
        while j < len(left):
          arr[i] = left[j]
          j += 1
          i += 1
        while k < len(right):
          arr[i] = right[k]
          k += 1
          i += 1

      def mergeSort(arr, l, r):
        if l == r: return arr
        m = (l + r) // 2
        mergeSort(arr, l, m)
        mergeSort(arr, m + 1, r)
        merge(arr, l, m, r)
        return arr

      return mergeSort(nums, 0, len(nums) - 1)

```
