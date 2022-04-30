# [1152. Analyze User Website Visit Pattern (Medium)](https://leetcode.com/problems/analyze-user-website-visit-pattern/)

<p>You are given two string arrays <code>username</code> and <code>website</code> and an integer array <code>timestamp</code>. All the given arrays are of the same length and the tuple <code>[username[i], website[i], timestamp[i]]</code> indicates that the user <code>username[i]</code> visited the website <code>website[i]</code> at time <code>timestamp[i]</code>.</p>

<p>A <strong>pattern</strong> is a list of three websites (not necessarily distinct).</p>

<ul>
	<li>For example, <code>["home", "away", "love"]</code>, <code>["leetcode", "love", "leetcode"]</code>, and <code>["luffy", "luffy", "luffy"]</code> are all patterns.</li>
</ul>

<p>The <strong>score</strong> of a <strong>pattern</strong> is the number of users that visited all the websites in the pattern in the same order they appeared in the pattern.</p>

<ul>
	<li>For example, if the pattern is <code>["home", "away", "love"]</code>, the score is the number of users <code>x</code> such that <code>x</code> visited <code>"home"</code> then visited <code>"away"</code> and visited <code>"love"</code> after that.</li>
	<li>Similarly, if the pattern is <code>["leetcode", "love", "leetcode"]</code>, the score is the number of users <code>x</code> such that <code>x</code> visited <code>"leetcode"</code> then visited <code>"love"</code> and visited <code>"leetcode"</code> <strong>one more time</strong> after that.</li>
	<li>Also, if the pattern is <code>["luffy", "luffy", "luffy"]</code>, the score is the number of users <code>x</code> such that <code>x</code> visited <code>"luffy"</code> three different times at different timestamps.</li>
</ul>

<p>Return <em>the <strong>pattern</strong> with the largest <strong>score</strong></em>. If there is more than one pattern with the same largest score, return the lexicographically smallest such pattern.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> username = ["joe","joe","joe","james","james","james","james","mary","mary","mary"], timestamp = [1,2,3,4,5,6,7,8,9,10], website = ["home","about","career","home","cart","maps","home","home","about","career"]
<strong>Output:</strong> ["home","about","career"]
<strong>Explanation:</strong> The tuples in this example are:
["joe","home",1],["joe","about",2],["joe","career",3],["james","home",4],["james","cart",5],["james","maps",6],["james","home",7],["mary","home",8],["mary","about",9], and ["mary","career",10].
The pattern ("home", "about", "career") has score 2 (joe and mary).
The pattern ("home", "cart", "maps") has score 1 (james).
The pattern ("home", "cart", "home") has score 1 (james).
The pattern ("home", "maps", "home") has score 1 (james).
The pattern ("cart", "maps", "home") has score 1 (james).
The pattern ("home", "home", "home") has score 0 (no user visited home 3 times).
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> username = ["ua","ua","ua","ub","ub","ub"], timestamp = [1,2,3,4,5,6], website = ["a","b","a","a","b","c"]
<strong>Output:</strong> ["a","b","a"]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= username.length &lt;= 50</code></li>
	<li><code>1 &lt;= username[i].length &lt;= 10</code></li>
	<li><code>timestamp.length == username.length</code></li>
	<li><code>1 &lt;= timestamp[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>website.length == username.length</code></li>
	<li><code>1 &lt;= website[i].length &lt;= 10</code></li>
	<li><code>username[i]</code> and <code>website[i]</code> consist of lowercase English letters.</li>
	<li>It is guaranteed that there is at least one user who visited at least three websites.</li>
	<li>All the tuples <code>[username[i], timestamp[i], website[i]]</code> are <strong>unique</strong>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Spotify](https://leetcode.com/company/spotify)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Sorting](https://leetcode.com/tag/sorting/)

## Solution 1.

```py
# OJ: https://leetcode.com/problems/analyze-user-website-visit-pattern/
# Author: Duy
# Time: O(N * C(N,K)), find combination cost C(N,K) with K = 3
# Space: O(N)
class Solution:
    def mostVisitedPattern(self, username: List[str], timestamp: List[int], website: List[str]) -> List[str]:
        arr = tuple(zip(timestamp, username, website))
        # print(arr)
        sarr = sorted(arr)
        userHistory = dict()
        for t,u,w in sarr:
            userHistory[u] = userHistory.get(u, list()) + [w]
        # print(userHistory)
        pattern = dict()
        for user in userHistory:
            hist = userHistory[user]
            # Use library function
            # combs = set(itertools.combinations(hist, 3))
            # or use custom function
            # The complexity is O(C(n,k)) which is O(n choose k).
            # This ends up being equivalent to O(min(n^k, n^(n-k))).
            combs = self.find3Comb(hist)
            for comb in combs:
                pattern[comb] = pattern.get(comb, 0) + 1
        #sort value desc, key asc => take first one
        #o(nlog) for sorting
        # return sorted(pattern, key = lambda x : (-pattern[x], x))[0]
        #o(n)
        res = tuple()
        count = 0
        for p in pattern:
            #if find better count or (same count but small lexicographically)
            if count < pattern[p] or (count == pattern[p] and p < res):
                count = pattern[p]
                res = p
        return res
    def find3Comb(self, hist):
        n = len(hist)
        res = set()
        count = 0
        for i in range(n - 2):
            for j in range(i+1, n - 1):
                for k in range(j+1, n):
                    r = (hist[i], hist[j], hist[k])
                    res.add(r)
                pattern[comb] = pattern.get(comb, 0) + 1
```
