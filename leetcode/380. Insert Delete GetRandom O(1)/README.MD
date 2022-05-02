# [380. Insert Delete GetRandom O(1) (Medium)](https://leetcode.com/problems/insert-delete-getrandom-o1/)

<p>Implement the <code>RandomizedSet</code> class:</p>

<ul>
	<li><code>RandomizedSet()</code> Initializes the <code>RandomizedSet</code> object.</li>
	<li><code>bool insert(int val)</code> Inserts an item <code>val</code> into the set if not present. Returns <code>true</code> if the item was not present, <code>false</code> otherwise.</li>
	<li><code>bool remove(int val)</code> Removes an item <code>val</code> from the set if present. Returns <code>true</code> if the item was present, <code>false</code> otherwise.</li>
	<li><code>int getRandom()</code> Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the <b>same probability</b> of being returned.</li>
</ul>

<p>You must implement the functions of the class such that each function works in&nbsp;<strong>average</strong>&nbsp;<code>O(1)</code>&nbsp;time complexity.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input</strong>
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
<strong>Output</strong>
[null, true, false, true, 2, true, false, 2]

<strong>Explanation</strong>
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomizedSet.remove(2); // Returns false as 2 does not exist in the set.
randomizedSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomizedSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomizedSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomizedSet.insert(2); // 2 was already in the set, so return false.
randomizedSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= val &lt;= 2<sup>31</sup> - 1</code></li>
	<li>At most <code>2 *&nbsp;</code><code>10<sup>5</sup></code> calls will be made to <code>insert</code>, <code>remove</code>, and <code>getRandom</code>.</li>
	<li>There will be <strong>at least one</strong> element in the data structure when <code>getRandom</code> is called.</li>
</ul>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [Bloomberg](https://leetcode.com/company/bloomberg), [Amazon](https://leetcode.com/company/amazon), [LinkedIn](https://leetcode.com/company/linkedin), [Microsoft](https://leetcode.com/company/microsoft), [Affirm](https://leetcode.com/company/affirm), [Uber](https://leetcode.com/company/uber), [Google](https://leetcode.com/company/google), [Twitter](https://leetcode.com/company/twitter), [Apple](https://leetcode.com/company/apple), [Tesla](https://leetcode.com/company/tesla), [Snapchat](https://leetcode.com/company/snapchat), [Oracle](https://leetcode.com/company/oracle), [Walmart Global Tech](https://leetcode.com/company/walmart-labs), [VMware](https://leetcode.com/company/vmware), [Indeed](https://leetcode.com/company/indeed), [Yandex](https://leetcode.com/company/yandex)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Math](https://leetcode.com/tag/math/), [Design](https://leetcode.com/tag/design/), [Randomized](https://leetcode.com/tag/randomized/)

**Similar Questions**:

- [Insert Delete GetRandom O(1) - Duplicates allowed (Hard)](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/insert-delete-getrandom-o1/
# Author: Duy Tran
# Time: O(1)
# Space: O(N)

class RandomizedSet:

    def __init__(self):
        #list to keep track the nums
        self.numList = list()

        #dict to keep track of position of num
        self.numDict = dict()

    # Append val into the last pos of numList
    # Keep track position of val
    def insert(self, val: int) -> bool:
        res = val not in self.numDict
        if res:
            self.numDict[val] = len(self.numList)
            self.numList.append(val)
        return res

    # Find the idx of val
    # Swap numList[val] and numList[-1]
    # Then remove val by pop the numList[-1] (which now contain val)
    def remove(self, val: int) -> bool:
        res = val in self.numDict
        if res:
            idx = self.numDict[val]
            lastVal = self.numList[-1]
            self.numList[idx] = lastVal
            self.numList.pop()
            self.numDict[lastVal] = idx
            del self.numDict[val]
        return res

    def getRandom(self) -> int:
        return random.choice(self.numList)



# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```
