[Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

# Intuition
The problem can be solved using depth-first search (DFS) on the border cells of the board. The idea is to identify the 'O' cells that are connected to the border cells and mark them as a special character ('*') to indicate that they should not be flipped to 'X'. After the DFS traversal, we iterate through the board and flip the remaining 'O' cells to 'X' and the '*' cells back to 'O'.

# Approach
1. Iterate through the first and last columns of the board and perform DFS on each 'O' cell encountered.
2. Iterate through the first and last rows of the board and perform DFS on each 'O' cell encountered.
3. During the DFS:
   - Check if the current cell is out of bounds or not an 'O' cell. If so, return.
   - Mark the current cell as visited by changing it to '*'.
   - Recursively perform DFS on the four adjacent cells (up, down, left, right).
4. After the DFS traversals, iterate through the entire board:
   - If a cell is 'O', flip it to 'X'.
   - If a cell is '*', flip it back to 'O'.

# Complexity
- Time complexity: O(rows * cols)
  - The DFS traversals visit each cell in the board at most once.
  - The iteration to flip the cells after the DFS also takes O(rows * cols) time.
  - Therefore, the overall time complexity is O(rows * cols).
- Space complexity: O(rows * cols)
  - The space complexity is determined by the recursion stack in the DFS traversal.
  - In the worst case, the DFS may go as deep as the number of cells in the board.
  - Therefore, the space complexity is O(rows * cols).

# Code
```java
class Solution {
    public void solve(char[][] board) {
        // perform dfs from the 'O' cells on the borders
        int rows = board.length, cols = board[0].length;
        for (int i = 0; i < rows; i++) {
            dfs(board, i, 0); // first column
            dfs(board, i, cols - 1); // last column
        }

        for (int i = 0; i < cols; i++) {
            dfs(board, 0, i); // first row
            dfs(board, rows - 1, i); // last row
        }

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                } else if (board[i][j] == '*') {
                    board[i][j] = 'O';
                }
            }
        }
    }

    private void dfs(char[][] board, int row, int col) {
        if (row < 0 || row >= board.length || col < 0 || col >= board[0].length || board[row][col] != 'O') {
            return;
        }
        board[row][col] = '*'; // marking them visited
        dfs(board, row + 1, col);
        dfs(board, row - 1, col);
        dfs(board, row, col + 1);
        dfs(board, row, col - 1);
    }
}
```