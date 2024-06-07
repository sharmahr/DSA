# Intuition
The problem asks to capture all the regions in the board that are not connected to the border and surrounded by 'X'. The intuition is to perform a depth-first search (DFS) starting from the 'O' cells on the borders and mark all the connected 'O' cells as a special character (e.g., '*'). After the DFS, all the remaining 'O' cells that are not marked as '*' are the ones that need to be captured and changed to 'X'.

# Approach
1. Iterate through the cells on the borders (first and last rows, first and last columns) of the board.
2. If a border cell is 'O', perform a DFS starting from that cell.
3. In the DFS:
   - If the current cell is out of bounds or is not 'O', return.
   - Mark the current cell as '*' to indicate that it is connected to the border.
   - Recursively explore the four adjacent cells (up, down, left, right).
4. After the DFS, iterate through each cell in the board.
   - If the cell is 'O', change it to 'X' as it is not connected to the border.
   - If the cell is '*', change it back to 'O' as it is connected to the border.

# Complexity
- Time complexity:
$$O(m \times n)$$, where m and n are the number of rows and columns in the board, respectively. Each cell is visited at most once during the DFS.

- Space complexity:
$$O(m \times n)$$ in the worst case, where the entire board is filled with 'O'. The recursion stack can go up to the size of the board.

# Code
```java
class Solution {
    public void solve(char[][] board) {
        int rows = board.length, cols = board[0].length;
        
        // Perform DFS from the 'O' cells on the borders
        for (int i = 0; i < rows; i++) {
            dfs(board, i, 0);          // First column
            dfs(board, i, cols - 1);   // Last column
        }
        for (int i = 0; i < cols; i++) {
            dfs(board, 0, i);          // First row
            dfs(board, rows - 1, i);   // Last row
        }
        
        // Update the board based on the DFS results
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
        
        board[row][col] = '*';  // Mark the cell as visited
        
        dfs(board, row - 1, col);  // Up
        dfs(board, row + 1, col);  // Down
        dfs(board, row, col - 1);  // Left
        dfs(board, row, col + 1);  // Right
    }
}
```