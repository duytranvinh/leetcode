# [567. Permutation in String (Medium)](https://leetcode.com/problems/permutation-in-string/)

<p>Given two strings <code>s1</code> and <code>s2</code>, return <code>true</code><em> if </em><code>s2</code><em> contains a permutation of </em><code>s1</code><em>, or </em><code>false</code><em> otherwise</em>.</p>

<p>In other words, return <code>true</code> if one of <code>s1</code>'s permutations is the substring of <code>s2</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> s1 = "ab", s2 = "eidbaooo"
<strong>Output:</strong> true
<strong>Explanation:</strong> s2 contains one permutation of s1 ("ba").
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> s1 = "ab", s2 = "eidboaoo"
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s1.length, s2.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s1</code> and <code>s2</code> consist of lowercase English letters.</li>
</ul>

**Companies**:  
[Microsoft](https://leetcode.com/company/microsoft), [Yandex](https://leetcode.com/company/yandex), [Amazon](https://leetcode.com/company/amazon), [Apple](https://leetcode.com/company/apple), [Google](https://leetcode.com/company/google), [Bloomberg](https://leetcode.com/company/bloomberg), [ByteDance](https://leetcode.com/company/bytedance), [Oracle](https://leetcode.com/company/oracle)

**Related Topics**:  
[Hash Table](https://leetcode.com/tag/hash-table/), [Two Pointers](https://leetcode.com/tag/two-pointers/), [String](https://leetcode.com/tag/string/), [Sliding Window](https://leetcode.com/tag/sliding-window/)

**Similar Questions**:

- [Minimum Window Substring (Hard)](https://leetcode.com/problems/minimum-window-substring/)
- [Find All Anagrams in a String (Medium)](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Solution 1. Sliding Window

We use sliding window with fix length `len(s1)`

At first, we build histogram for `s1` and `s2` with length of `s1`

We keep track the number of `matches` in the histogram

We keep sliding to find the `matches`

At any time, if `matches == 26`, mean all character count is matched. We return `True`
e

```py
# OJ: https://leetcode.com/problems/permutation-in-string/
# Author: Duy Tran
# Time: O(N)
# Space: O(1) or O(26)

class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2): return False

        s1Count, s2Count = [0 for _ in range(26)], [0 for _ in range(26)]
        for i in range(len(s1)):
            s1Count[ord(s1[i]) - ord('a')] += 1
            s2Count[ord(s2[i]) - ord('a')] += 1

        matches = 0
        for i in range(26):
            matches += 1 if s1Count[i] == s2Count[i] else 0

        l, r = 0, len(s1)
        while r < len(s2):
            if matches == 26: return True

            index = ord(s2[r]) - ord('a')
            s2Count[index] += 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            # else if they were equal, but we increase our s2Count[index] so it is unequal
            # so we have to decrease our matches
            elif s1Count[index] + 1 == s2Count[index]:
                matches -= 1
            r += 1

            index = ord(s2[l]) - ord('a')
            s2Count[index] -= 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            # else if they were equal, but we decrease our s2Count[index] so it is unequal
            # so we have to decrease our matches
            elif s1Count[index] - 1 == s2Count[index]:
                matches -= 1
            l += 1

        return matches == 26

```

## Solution 2. Sliding Window with Hashmap

Although this code is easier to read, it is not sufficient

Since we have to check `c in s1Count`, it cost `O(s1Count) = number of unique character in s1`, which is `O(M)` at the worst case

Although `O(M)` can only be maximum `O(26)`

But the previous solution only cost `O(1)` to check for the count

```py
# OJ: https://leetcode.com/problems/permutation-in-string/
# Author: Duy Tran
# Time: O(N*M)
# Space: O(M)

        return matches == len(s1)
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2): return False

        s1Count, s2Count = defaultdict(int), defaultdict(int)
        for i in range(len(s1)):
            s1Count[s1[i]] += 1
            s2Count[s2[i]] += 1

        matches = 0
        for c in s1Count:
            matches += 1 if (c in s2Count and s2Count[c] == s1Count[c]) else 0

        l, r = 0, len(s1)
        while r < len(s2):
            if matches == len(s1Count): return True

            c = s2[r]
            s2Count[c] += 1
            if c in s1Count:
                if s1Count[c] == s2Count[c]:
                    matches += 1
                # else if they were equal, but we increase our s2Count[index] so it is unequal
                # so we have to decrease our matches
                elif s1Count[c] + 1 == s2Count[c]:
                    matches -= 1
            r += 1

            c = s2[l]
            s2Count[c] -= 1
            if c in s1Count:
                if s1Count[c] == s2Count[c]:
                    matches += 1
                # else if they were equal, but we decrease our s2Count[index] so it is unequal
                # so we have to decrease our matches
                elif s1Count[c] - 1 == s2Count[c]:
                    matches -= 1
            l += 1

        return matches == len(s1Count)
```
