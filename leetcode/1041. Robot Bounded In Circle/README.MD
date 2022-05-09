# [1041. Robot Bounded In Circle (Medium)](https://leetcode.com/problems/robot-bounded-in-circle/)

<p>On an infinite plane, a robot initially stands at <code>(0, 0)</code> and faces north. Note that:</p>

<ul>
	<li>The <strong>north direction</strong> is the positive direction of the y-axis.</li>
	<li>The <strong>south direction</strong> is the negative direction of the y-axis.</li>
	<li>The <strong>east direction</strong> is the positive direction of the x-axis.</li>
	<li>The <strong>west direction</strong> is the negative direction of the x-axis.</li>
</ul>

<p>The robot can receive one of three instructions:</p>

<ul>
	<li><code>"G"</code>: go straight 1 unit.</li>
	<li><code>"L"</code>: turn 90 degrees to the left (i.e., anti-clockwise direction).</li>
	<li><code>"R"</code>: turn 90 degrees to the right (i.e., clockwise direction).</li>
</ul>

<p>The robot performs the <code>instructions</code> given in order, and repeats them forever.</p>

<p>Return <code>true</code> if and only if there exists a circle in the plane such that the robot never leaves the circle.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> instructions = "GGLLGG"
<strong>Output:</strong> true
<strong>Explanation:</strong> The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"G": move one step. Position: (0, 2). Direction: North.
"L": turn 90 degrees anti-clockwise. Position: (0, 2). Direction: West.
"L": turn 90 degrees anti-clockwise. Position: (0, 2). Direction: South.
"G": move one step. Position: (0, 1). Direction: South.
"G": move one step. Position: (0, 0). Direction: South.
Repeating the instructions, the robot goes into the cycle: (0, 0) --&gt; (0, 1) --&gt; (0, 2) --&gt; (0, 1) --&gt; (0, 0).
Based on that, we return true.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> instructions = "GG"
<strong>Output:</strong> false
<strong>Explanation:</strong> The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"G": move one step. Position: (0, 2). Direction: North.
Repeating the instructions, keeps advancing in the north direction and does not go into cycles.
Based on that, we return false.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> instructions = "GL"
<strong>Output:</strong> true
<strong>Explanation:</strong> The robot is initially at (0, 0) facing the north direction.
"G": move one step. Position: (0, 1). Direction: North.
"L": turn 90 degrees anti-clockwise. Position: (0, 1). Direction: West.
"G": move one step. Position: (-1, 1). Direction: West.
"L": turn 90 degrees anti-clockwise. Position: (-1, 1). Direction: South.
"G": move one step. Position: (-1, 0). Direction: South.
"L": turn 90 degrees anti-clockwise. Position: (-1, 0). Direction: East.
"G": move one step. Position: (0, 0). Direction: East.
"L": turn 90 degrees anti-clockwise. Position: (0, 0). Direction: North.
Repeating the instructions, the robot goes into the cycle: (0, 0) --&gt; (0, 1) --&gt; (-1, 1) --&gt; (-1, 0) --&gt; (0, 0).
Based on that, we return true.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= instructions.length &lt;= 100</code></li>
	<li><code>instructions[i]</code> is <code>'G'</code>, <code>'L'</code> or, <code>'R'</code>.</li>
</ul>

**Companies**:  
[Goldman Sachs](https://leetcode.com/company/goldman-sachs), [Amazon](https://leetcode.com/company/amazon), [Bloomberg](https://leetcode.com/company/bloomberg), [Adobe](https://leetcode.com/company/adobe)

**Related Topics**:  
[Math](https://leetcode.com/tag/math/), [String](https://leetcode.com/tag/string/), [Simulation](https://leetcode.com/tag/simulation/)

## Solution 1.

After one complete cycle,

If it's facing north or at origin, then it's a cycle

```py
# OJ: https://leetcode.com/problems/robot-bounded-in-circle/
# Author: Duy Tran
# Time: O(N)
# Space: O(1)

class Solution:
    def isRobotBounded(self, instructions: str) -> bool:
        #north = 0, east = 1, south = 2, west = 3
        dir = [[0,1], [1,0], [0, -1], [-1, 0]]
        x, y, idx = 0, 0, 0
        for instruction in instructions:
            if(instruction == 'L'):
                idx = (idx + 3) % 4
            elif(instruction == 'R'):
                idx = (idx + 1) % 4
            else:
                x += dir[idx][0]
                y += dir[idx][1]
        return (x == 0 and y == 0) or (idx != 0)

```
