# [169. Majority Element (Easy)](https://leetcode.com/problems/majority-element)

<p>Given an array <code>nums</code> of size <code>n</code>, return <em>the majority element</em>.</p>

<p>The majority element is the element that appears more than <code>&lfloor;n / 2&rfloor;</code> times. You may assume that the majority element always exists in the array.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [3,2,3]
<strong>Output:</strong> 3
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [2,2,1,1,1,2,2]
<strong>Output:</strong> 2
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow-up:</strong> Could you solve the problem in linear time and in <code>O(1)</code> space?

**Companies**:
[Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Bloomberg](https://leetcode.com/company/bloomberg), [Google](https://leetcode.com/company/google), [Adobe](https://leetcode.com/company/adobe), [Facebook](https://leetcode.com/company/facebook), [Microsoft](https://leetcode.com/company/microsoft), [Salesforce](https://leetcode.com/company/salesforce), [Pwc](https://leetcode.com/company/pwc), [Uber](https://leetcode.com/company/uber), [eBay](https://leetcode.com/company/ebay), [Nvidia](https://leetcode.com/company/nvidia), [tcs](https://leetcode.com/company/tcs), [Yandex](https://leetcode.com/company/yandex), [Media.net](https://leetcode.com/company/medianet), [Deutsche Bank](https://leetcode.com/company/deutsche-bank), [Zenefits](https://leetcode.com/company/zenefits)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [Divide and Conquer](https://leetcode.com/tag/divide-and-conquer), [Sorting](https://leetcode.com/tag/sorting), [Counting](https://leetcode.com/tag/counting)

**Similar Questions**:

- [Majority Element II (Medium)](https://leetcode.com/problems/majority-element-ii)
- [Check If a Number Is Majority Element in a Sorted Array (Easy)](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array)
- [Most Frequent Even Element (Easy)](https://leetcode.com/problems/most-frequent-even-element)
- [Minimum Index of a Valid Split (Medium)](https://leetcode.com/problems/minimum-index-of-a-valid-split)
- [Minimum Operations to Exceed Threshold Value I (Easy)](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-i)

## Solution 1.

Build hashmap with key = n and value is count

Loop through and find the largest count

```py
# OJ: https://leetcode.com/problems/majority-element
# Author: Duy Tran
# Time: O(N)
# Space: O(N)

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        hist = defaultdict(int)
        res, maxCount = 0, 0
        for n in nums:
          hist[n] += 1
          res = n if hist[n] > maxCount else res
          maxCount = max(hist[n], maxCount)
        return res

```

## Solution 2: Boyer-Moore Voting Algorithm

### Intuition

<p>If we had some way of counting instances of the majority element as <span class="math math-inline"><span class="katex"><span class="katex-mathml">+1+1</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.7278em; vertical-align: -0.0833em;"></span><span class="mord">+</span><span class="mord">1</span></span></span></span></span><br>
and instances of any other element as <span class="math math-inline"><span class="katex"><span class="katex-mathml">−1-1</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.7278em; vertical-align: -0.0833em;"></span><span class="mord">−</span><span class="mord">1</span></span></span></span></span>, summing them would make it<br>
obvious that the majority element is indeed the majority element.</p>

### Algorithm

<p>Essentially, what Boyer-Moore does is look for a suffix <span class="math math-inline"><span class="katex"><span class="katex-mathml">sufsuf</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.8889em; vertical-align: -0.1944em;"></span><span class="mord mathnormal">s</span><span class="mord mathnormal">u</span><span class="mord mathnormal" style="margin-right: 0.10764em;">f</span></span></span></span></span> of <code>nums</code><br>
where <span class="math math-inline"><span class="katex"><span class="katex-mathml">suf[0]suf[0]</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal">s</span><span class="mord mathnormal">u</span><span class="mord mathnormal" style="margin-right: 0.10764em;">f</span><span class="mopen">[</span><span class="mord">0</span><span class="mclose">]</span></span></span></span></span> is the majority element in that suffix. To do this, we<br>
maintain a count, which is incremented whenever we see an instance of our<br>
current candidate for majority element and decremented whenever we see<br>
anything else. Whenever <code>count</code> equals 0, we effectively forget about<br>
everything in <code>nums</code> up to the current index and consider the current number<br>
as the candidate for majority element. It is not immediately obvious why we can<br>
get away with forgetting prefixes of <code>nums</code> - consider the following<br>
examples (pipes are inserted to separate runs of nonzero <code>count</code>).</p>

<p>[7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | 7, 7, 7, 7]</p>

<p>Here, the <code>7</code> at index 0 is selected to be the first candidate for majority<br>
element. <code>count</code> will eventually reach 0 after index 5 is processed, so the<br>
<code>5</code> at index 6 will be the next candidate. In this case, <code>7</code> is the true<br>
majority element, so by disregarding this prefix, we are ignoring an equal<br>
number of majority and minority elements - therefore, <code>7</code> will still be the<br>
majority element in the suffix formed by throwing away the first prefix.</p>

<p>[7, 7, 5, 7, 5, 1 | 5, 7 | 5, 5, 7, 7 | <strong>5, 5, 5, 5</strong>]</p>

<p>Now, the majority element is <code>5</code> (we changed the last run of the array from<br>
<code>7</code>s to <code>5</code>s), but our first candidate is still <code>7</code>. In this case, our<br>
candidate is not the true majority element, but we still cannot discard more<br>
majority elements than minority elements (this would imply that <code>count</code> could<br>
reach -1 before we reassign <code>candidate</code>, which is obviously false).</p>

<p>Therefore, given that it is impossible (in both cases) to discard more<br>
majority elements than minority elements, we are safe in discarding the<br>
prefix and attempting to recursively solve the majority element problem for the<br>
suffix. Eventually, a suffix will be found for which <code>count</code> does not hit<br>
<code>0</code>, and the majority element of that suffix will necessarily be the same as<br>
the majority element of the overall array.</p>

### Human Explanation

A majority element is a number that occur more than half of array size.

Since it is guarantee that the majority element always exists in the array.

We can leverage this by counting a candidate number

Given a candidate number (starting with the first number in the array), if current `num` is a candidate, then we add `1` to `count`, else `-1` to `count`

If `count === 0`, we got a new candidate number.

Given the array `1 1 2 2 2`, the candidate is `1 1 1 1 2` and `count` is updating as `1 2 3 2 1 0`

`1 1 2 2 3 3 3 3` the candidate is `1 1 1 1 3 3 3 3` and the `count` is updating as `1 2 1 0 1 2 3 4`

Again, this works because the is always a majority element in the array

### Implementation

```py
class Solution:
    def majorityElement(self, nums):
        count = 0
        candidate = None

        for num in nums:
            if count == 0:
                candidate = num
            count += (1 if num == candidate else -1)

        return candidate
```

### Complexity Analysis

<ul>
<li>
<p>Time complexity : <span class="math math-inline"><span class="katex"><span class="katex-mathml">O(n)O(n)</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.02778em;">O</span><span class="mopen">(</span><span class="mord mathnormal">n</span><span class="mclose">)</span></span></span></span></span></p>
<p>Boyer-Moore performs constant work exactly <span class="math math-inline"><span class="katex"><span class="katex-mathml">nn</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.4306em;"></span><span class="mord mathnormal">n</span></span></span></span></span> times, so the algorithm<br>
runs in linear time.</p>
</li>
<li>
<p>Space complexity : <span class="math math-inline"><span class="katex"><span class="katex-mathml">O(1)O(1)</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.02778em;">O</span><span class="mopen">(</span><span class="mord">1</span><span class="mclose">)</span></span></span></span></span></p>
<p>Boyer-Moore allocates only constant additional memory.</p>
</li>
</ul>
