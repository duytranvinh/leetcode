# [36. Valid Sudoku (Medium)](https://leetcode.com/problems/valid-sudoku/)

<p>Determine if a&nbsp;<code>9 x 9</code> Sudoku board&nbsp;is valid.&nbsp;Only the filled cells need to be validated&nbsp;<strong>according to the following rules</strong>:</p>

<ol>
	<li>Each row&nbsp;must contain the&nbsp;digits&nbsp;<code>1-9</code> without repetition.</li>
	<li>Each column must contain the digits&nbsp;<code>1-9</code>&nbsp;without repetition.</li>
	<li>Each of the nine&nbsp;<code>3 x 3</code> sub-boxes of the grid must contain the digits&nbsp;<code>1-9</code>&nbsp;without repetition.</li>
</ol>

<p><strong>Note:</strong></p>

<ul>
	<li>A Sudoku board (partially filled) could be valid but is not necessarily solvable.</li>
	<li>Only the filled cells need to be validated according to the mentioned&nbsp;rules.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" style="height:250px; width:250px">
<pre><strong>Input:</strong> board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
<strong>Output:</strong> true
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
<strong>Output:</strong> false
<strong>Explanation:</strong> Same as Example 1, except with the <strong>5</strong> in the top left corner being modified to <strong>8</strong>. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>board.length == 9</code></li>
	<li><code>board[i].length == 9</code></li>
	<li><code>board[i][j]</code> is a digit <code>1-9</code> or <code>'.'</code>.</li>
</ul>

**Companies**:  
[Amazon](https://leetcode.com/company/amazon), [Uber](https://leetcode.com/company/uber), [Microsoft](https://leetcode.com/company/microsoft), [Apple](https://leetcode.com/company/apple), [Karat](https://leetcode.com/company/karat), [Facebook](https://leetcode.com/company/facebook), [Wayfair](https://leetcode.com/company/wayfair), [Nvidia](https://leetcode.com/company/nvidia), [Cruise Automation](https://leetcode.com/company/cruise-automation), [Qualtrics](https://leetcode.com/company/qualtrics)

**Related Topics**:  
[Array](https://leetcode.com/tag/array/), [Hash Table](https://leetcode.com/tag/hash-table/), [Matrix](https://leetcode.com/tag/matrix/)

**Similar Questions**:

- [Sudoku Solver (Hard)](https://leetcode.com/problems/sudoku-solver/)
- [Check if Every Row and Column Contains All Numbers (Easy)](https://leetcode.com/problems/check-if-every-row-and-column-contains-all-numbers/)

## Solution 1.

Use a `hash map` to keep track of each row, column and grid `map<int, set>`

We calculate grid by `key = (r /3, c /3)`

```py
# OJ: https://leetcode.com/problems/valid-sudoku/
# Author: Duy Tran
# Time: O(N) => size of the board
# Space: O(N) => size of the board

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        squares = collections.defaultdict(set) # key = (r /3, c /3)

        m = len(board[0])
        n = len(board)
        for r in range(9):
            for c in range(9):
                cur = board[r][c]
                if cur == ".":
                    continue
                if (cur in rows[r] or
                    cur in cols[c] or
                    cur in squares[(r // 3, c // 3)]):
                    return False
                cols[c].add(cur)
                rows[r].add(cur)
                squares[(r // 3, c // 3)].add(cur)

        return True

```

Javascript

```js
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function (board) {
  m = board[0].length;
  n = board.length;
  const cols = getBoard(n);
  const rows = getBoard(n);
  const squares = getBoard(n);

  for (let r = 0; r < n; r++) {
    for (let c = 0; c < m; c++) {
      const cur = board[r][c];
      if (cur === ".") {
        continue;
      }
      const box = Math.floor(r / 3) * 3 + Math.floor(c / 3);
      if (cols[c].has(cur) || rows[r].has(cur) || squares[box].has(cur)) {
        return false;
      }
      cols[c].add(cur);
      rows[r].add(cur);
      squares[box].add(cur);
    }
  }

  return true;
};

const getBoard = (n) => {
  const arr = new Array(n).fill();
  return arr.map(() => new Set());
};
```

Javascript

```js
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function (board) {
  m = board[0].length;
  n = board.length;
  const cols = getBoard(n);
  const rows = getBoard(n);
  const squares = getBoard(n);
  for (let r = 0; r < n; r++) {
    for (let c = 0; c < m; c++) {
      const cur = board[r][c];
      const box = Math.floor(r / 3) * 3 + Math.floor(c / 3);
      if (cur !== ".") {
        cols[c].add(cur);
        rows[r].add(cur);
        squares[box].add(cur);
      }
    }
  }
  dfs(board, cols, rows, squares);
};

const dfs = (board, cols, rows, squares) => {
  const n = board.length;
  const m = board[0].length;
  for (let r = 0; r < n; r++) {
    for (let c = 0; c < m; c++) {
      const cur = board[r][c];
      if (cur !== ".") {
        continue;
      }
      const box = Math.floor(r / 3) * 3 + Math.floor(c / 3);
      for (let i = 1; i <= n; i++) {
        const curNum = String(i);
        if (isValid(board, r, c, curNum, cols, rows, squares)) {
          board[r][c] = curNum;
          cols[c].add(curNum);
          rows[r].add(curNum);
          squares[box].add(curNum);
          if (dfs(board, cols, rows, squares)) return true;
          cols[c].delete(curNum);
          rows[r].delete(curNum);
          squares[box].delete(curNum);
        }
      }
      board[r][c] = ".";
      return false;
    }
  }
  return true;
};

const isValid = (board, r, c, curNum, cols, rows, squares) => {
  const box = Math.floor(r / 3) * 3 + Math.floor(c / 3);
  if (cols[c].has(curNum) || rows[r].has(curNum) || squares[box].has(curNum)) {
    return false;
  }
  return true;
};

const getBoard = (n) => {
  const arr = new Array(n).fill();
  return arr.map(() => new Set());
};
```
