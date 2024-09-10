# [37. Sudoku Solver (Hard)](https://leetcode.com/problems/sudoku-solver)

<p>Write a program to solve a Sudoku puzzle by filling the empty cells.</p>

<p>A sudoku solution must satisfy <strong>all of the following rules</strong>:</p>

<ol>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each row.</li>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each column.</li>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each of the 9 <code>3x3</code> sub-boxes of the grid.</li>
</ol>

<p>The <code>&#39;.&#39;</code> character indicates empty cells.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" style="height:250px; width:250px" />
<pre>
<strong>Input:</strong> board = [[&quot;5&quot;,&quot;3&quot;,&quot;.&quot;,&quot;.&quot;,&quot;7&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;],[&quot;6&quot;,&quot;.&quot;,&quot;.&quot;,&quot;1&quot;,&quot;9&quot;,&quot;5&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;],[&quot;.&quot;,&quot;9&quot;,&quot;8&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;6&quot;,&quot;.&quot;],[&quot;8&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;6&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;3&quot;],[&quot;4&quot;,&quot;.&quot;,&quot;.&quot;,&quot;8&quot;,&quot;.&quot;,&quot;3&quot;,&quot;.&quot;,&quot;.&quot;,&quot;1&quot;],[&quot;7&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;2&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;6&quot;],[&quot;.&quot;,&quot;6&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;2&quot;,&quot;8&quot;,&quot;.&quot;],[&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;4&quot;,&quot;1&quot;,&quot;9&quot;,&quot;.&quot;,&quot;.&quot;,&quot;5&quot;],[&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;.&quot;,&quot;8&quot;,&quot;.&quot;,&quot;.&quot;,&quot;7&quot;,&quot;9&quot;]]
<strong>Output:</strong> [[&quot;5&quot;,&quot;3&quot;,&quot;4&quot;,&quot;6&quot;,&quot;7&quot;,&quot;8&quot;,&quot;9&quot;,&quot;1&quot;,&quot;2&quot;],[&quot;6&quot;,&quot;7&quot;,&quot;2&quot;,&quot;1&quot;,&quot;9&quot;,&quot;5&quot;,&quot;3&quot;,&quot;4&quot;,&quot;8&quot;],[&quot;1&quot;,&quot;9&quot;,&quot;8&quot;,&quot;3&quot;,&quot;4&quot;,&quot;2&quot;,&quot;5&quot;,&quot;6&quot;,&quot;7&quot;],[&quot;8&quot;,&quot;5&quot;,&quot;9&quot;,&quot;7&quot;,&quot;6&quot;,&quot;1&quot;,&quot;4&quot;,&quot;2&quot;,&quot;3&quot;],[&quot;4&quot;,&quot;2&quot;,&quot;6&quot;,&quot;8&quot;,&quot;5&quot;,&quot;3&quot;,&quot;7&quot;,&quot;9&quot;,&quot;1&quot;],[&quot;7&quot;,&quot;1&quot;,&quot;3&quot;,&quot;9&quot;,&quot;2&quot;,&quot;4&quot;,&quot;8&quot;,&quot;5&quot;,&quot;6&quot;],[&quot;9&quot;,&quot;6&quot;,&quot;1&quot;,&quot;5&quot;,&quot;3&quot;,&quot;7&quot;,&quot;2&quot;,&quot;8&quot;,&quot;4&quot;],[&quot;2&quot;,&quot;8&quot;,&quot;7&quot;,&quot;4&quot;,&quot;1&quot;,&quot;9&quot;,&quot;6&quot;,&quot;3&quot;,&quot;5&quot;],[&quot;3&quot;,&quot;4&quot;,&quot;5&quot;,&quot;2&quot;,&quot;8&quot;,&quot;6&quot;,&quot;1&quot;,&quot;7&quot;,&quot;9&quot;]]
<strong>Explanation:</strong>&nbsp;The input board is shown above and the only valid solution is shown below:

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png" style="height:250px; width:250px" />
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>board.length == 9</code></li>
	<li><code>board[i].length == 9</code></li>
	<li><code>board[i][j]</code> is a digit or <code>&#39;.&#39;</code>.</li>
	<li>It is <strong>guaranteed</strong> that the input board has only one solution.</li>
</ul>

**Companies**:
[Microsoft](https://leetcode.com/company/microsoft), [Google](https://leetcode.com/company/google), [Amazon](https://leetcode.com/company/amazon), [Intuit](https://leetcode.com/company/intuit), [Zoho](https://leetcode.com/company/zoho), [Adobe](https://leetcode.com/company/adobe), [Citadel](https://leetcode.com/company/citadel), [Apple](https://leetcode.com/company/apple), [Riot Games](https://leetcode.com/company/riot-games), [DoorDash](https://leetcode.com/company/doordash), [Confluent](https://leetcode.com/company/confluent), [Bloomberg](https://leetcode.com/company/bloomberg), [Oracle](https://leetcode.com/company/oracle), [Cadence](https://leetcode.com/company/cadence), [Uber](https://leetcode.com/company/uber), [Snap](https://leetcode.com/company/snapchat)

**Related Topics**:  
[Array](https://leetcode.com/tag/array), [Hash Table](https://leetcode.com/tag/hash-table), [Backtracking](https://leetcode.com/tag/backtracking), [Matrix](https://leetcode.com/tag/matrix)

**Similar Questions**:

- [Valid Sudoku (Medium)](https://leetcode.com/problems/valid-sudoku)
- [Unique Paths III (Hard)](https://leetcode.com/problems/unique-paths-iii)

## Solution 1. DFS / Backtracking

### Algorithm

We will use DFS or Backtracking to solve this problem

<ul>
<li>
<p>Start from the upper left cell <code>row = 0, col = 0</code>. Proceed till the first free cell.</p>
</li>
<li>
<p>Iterate over the numbers from <code>1</code> to <code>9</code> and try to put each number <code>cur</code> in the <code>(row, col)</code> cell.</p>
<ul>
<li>
<p>If number <code>cur</code> is not yet in the current row, column, and box:</p>
<ul>
<li>Place the <code>cur</code> in a <code>(row, col)</code> cell.</li>
<li>If we're on the last cell <code>row == 8, col == 8</code>:
<ul>
<li>That means that we've solved the sudoku.</li>
</ul>
</li>
<li>Else
<ul>
<li>Proceed to place further numbers.</li>
</ul>
</li>
<li>Backtrack if the solution is not yet here: remove the last number from the <code>(row, col)</code> cell.</li>
</ul>
</li>
</ul>
</li>
</ul>

### Solution 1a: Loop through Array to check

How to check if the `cur` number is valid

- Loop from 1 to 9

  - Check if the `cur` number already in row 1 to 9

  - Check if the `cur` number already in col 1 to 9

  - Check if the `cur` number already in its block

    - Need to find its block first

      - `blockRow = (r // 3) * 3` and `blockCol = (c // 3) * 3`

    - And then in each iteration, we check the block

      - `curBlockRow = blockRow + (i // 3)` and `curBlockCol = blockCol + (i % 3)`
      - if `board[curBlockRow][curBlockCol] == cur` return `False`

Python

```py
# OJ: https://leetcode.com/problems/sudoku-solver
# Author: Duy Tran
# Time: O(9!)^9 or O(1) since there is fixed number of space
# Space: O(1), no need extra space

class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        self.dfs(board)

    def dfs(self, board):
      n = len(board)
      m = len(board[0])
      for r in range(n):
        for c in range(m):
          if board[r][c] != '.': continue
          for i in range(1, 10):
            cur = str(i)
            if (self.isValid(board, r, c, cur)):
              board[r][c] = cur
              if (self.dfs(board)): return True
          board[r][c] = '.'
          return False
      return True


    def isValid(self, board, r, c, cur):
      n = len(board)
      blockRow = (r // 3) * 3
      blockCol = (c // 3) * 3
      for i in range(n):
        if (board[r][i] == cur or board[i][c] == cur): return False
        curBlockRow = blockRow + (i // 3)
        curBlockCol = blockCol + (i % 3)
        if board[curBlockRow][curBlockCol] == cur: return False
      return True
```

Javascript

```js
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function (board) {
  dfs(board);
};

const dfs = (board) => {
  const n = board.length;
  const m = board[0].length;
  for (let r = 0; r < n; r++) {
    for (let c = 0; c < m; c++) {
      if (board[r][c] !== ".") {
        continue;
      }
      for (let i = 1; i <= n; i++) {
        const cur = String(i);
        if (isValid(board, r, c, cur)) {
          board[r][c] = cur;
          if (dfs(board)) return true;
        }
      }
      board[r][c] = ".";
      return false;
    }
  }
  return true;
};

const isValid = (board, r, c, cur) => {
  n = board.length;
  const blockRow = Math.floor(r / 3) * 3;
  const blockCol = Math.floor(c / 3) * 3;
  for (let i = 0; i < n; i++) {
    if (board[r][i] === cur || board[i][c] === cur) return false;
    const curBlockRow = blockRow + Math.floor(i / 3);
    const curBlockCol = blockCol + (i % 3);
    if (board[curBlockRow][curBlockCol] === cur) return false;
  }
  return true;
};
```

### Solution 1b: Use a Set to keep track of filled number

How to check if the `cur` number is valid

- In this solution, we create maps of sets for each `cols, rows , squares`

- Then we have to prefill the map with the original unsolved sudoku

- We need to do that so that when iterating through each number, we will be able to know if that number is valid or not.

- Then we can check if `cur` number is in the set or not

- For each `cur` valid number, we add it to the set

- If that `cur` number is valid but that path is not working, then we remove the number out of the set

```py
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        n = len(board)
        m = len(board[0])
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        squares = collections.defaultdict(set)
        for r in range(n):
          for c in range(m):
            cur = board[r][c]
            box = (r // 3) * 3 + (c // 3)
            if cur != '.':
              rows[r].add(cur)
              cols[c].add(cur)
              squares[box].add(cur)

        self.dfs(board, cols, rows, squares)

    def dfs(self, board, cols, rows, squares):
      n = len(board)
      m = len(board[0])
      for r in range(n):
        for c in range(m):
          cur = board[r][c]
          if cur != '.':
            continue
          box = (r // 3) * 3 + (c // 3)
          for i in range(1, 10):
            curNum = str(i)
            if (self.isValid(board, r, c, curNum, cols, rows, squares)):
              board[r][c] = curNum
              rows[r].add(curNum)
              cols[c].add(curNum)
              squares[box].add(curNum)
              if (self.dfs(board, cols, rows, squares)): return True
              rows[r].remove(curNum)
              cols[c].remove(curNum)
              squares[box].remove(curNum)
          board[r][c] = '.'
          return False
      return True


    def isValid(self, board, r, c, curNum, cols, rows, squares):
      box = (r // 3) * 3 + (c // 3)
      if (curNum in rows[r] or
          curNum in cols[c] or
          curNum in squares[box]):
          return False
      return True
```
