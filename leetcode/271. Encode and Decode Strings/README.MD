# [271. Encode and Decode Strings (Medium)](https://leetcode.com/problems/encode-and-decode-strings/)

<p>Design an algorithm to encode <b>a list of strings</b> to <b>a string</b>. The encoded string is then sent over the network and is decoded back to the original list of strings.</p>

<p>Machine 1 (sender) has the function:</p>

<pre>string encode(vector&lt;string&gt; strs) {
  // ... your code
  return encoded_string;
}</pre>

Machine 2 (receiver) has the function:

<pre>vector&lt;string&gt; decode(string s) {
  //... your code
  return strs;
}
</pre>

<p>So Machine 1 does:</p>

<pre>string encoded_string = encode(strs);
</pre>

<p>and Machine 2 does:</p>

<pre>vector&lt;string&gt; strs2 = decode(encoded_string);
</pre>

<p><code>strs2</code> in Machine 2 should be the same as <code>strs</code> in Machine 1.</p>

<p>Implement the <code>encode</code> and <code>decode</code> methods.</p>

<p>You are not allowed to&nbsp;solve the problem using any serialize methods (such as <code>eval</code>).</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> dummy_input = ["Hello","World"]
<strong>Output:</strong> ["Hello","World"]
<strong>Explanation:</strong>
Machine 1:
Codec encoder = new Codec();
String msg = encoder.encode(strs);
Machine 1 ---msg---&gt; Machine 2

Machine 2:
Codec decoder = new Codec();
String[] strs = decoder.decode(msg);
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> dummy_input = [""]
<strong>Output:</strong> [""]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 200</code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 200</code></li>
	<li><code>strs[i]</code> contains any possible characters out of <code>256</code> valid ASCII characters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up: </strong>Could you write a generalized algorithm to work on any possible set of characters?</p>

**Companies**:  
[Facebook](https://leetcode.com/company/facebook), [LinkedIn](https://leetcode.com/company/linkedin)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [String](https://leetcode.com/tag/string/), [Design](https://leetcode.com/tag/design/)

**Similar Questions**:

- [Count and Say (Medium)](https://leetcode.com/problems/count-and-say/)
- [Serialize and Deserialize Binary Tree (Hard)](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
- [String Compression (Medium)](https://leetcode.com/problems/string-compression/)
- [Count Binary Substrings (Easy)](https://leetcode.com/problems/count-binary-substrings/)

## Solution 1.

Encode to `len + # + s` for each `s`

```py
# OJ: https://leetcode.com/problems/encode-and-decode-strings/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        res = list()
        for s in strs:
            r = str(len(s)) + '#' + s
            res.append(r)
        return "".join(res)
    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        res, start = list(), 0

        while start < len(s):
            j = start

            while s[j] != '#':
                j += 1

            #grab the length of word, sometime there's multiple digits length
            length = int(s[start:j])

            res.append(s[j + 1: j + 1 + length])
            start = j + 1 + length
        return res

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```
