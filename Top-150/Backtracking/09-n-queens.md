[N Queens](https://leetcode.com/problems/n-queens/description/)

# Intuition
The N-Queens problem can be solved using a backtracking approach. The intuition is to place queens on the chessboard row by row, and for each row, we try placing the queen in each column. We need to ensure that no two queens attack each other, i.e., no two queens share the same row, column, or diagonal. We can use boolean arrays to keep track of the columns and diagonals that are already occupied by queens.

# Approach
1. Create an empty result list to store all the valid solutions.
2. Initialize a 2D character array `board` of size `n x n` to represent the chessboard, initially filled with '.' to represent empty cells.
3. Create boolean arrays `cols`, `diag1`, and `diag2` to keep track of the columns, main diagonals, and anti-diagonals that are occupied by queens.
4. Define a recursive function `backtrack` that takes the following parameters:
   - `row`: The current row being processed.
   - `n`: The size of the chessboard.
   - `board`: The 2D character array representing the chessboard.
   - `cols`, `diag1`, `diag2`: The boolean arrays to keep track of occupied columns and diagonals.
   - `result`: The list to store all the valid solutions.
5. In the `backtrack` function:
   - Base case: If `row` equals `n`, it means all rows have been processed and a valid solution is found. Convert the `board` to a list of strings using the `constructBoard` function and add it to the `result` list. Return.
   - Iterate through each column in the current row:
     - Check if the current column and diagonals are not occupied by queens.
     - If the column and diagonals are free, place a queen ('Q') at the current position on the `board`, mark the corresponding column and diagonals as occupied, and recursively call `backtrack` for the next row.
     - After the recursive call, remove the queen from the current position, and mark the corresponding column and diagonals as unoccupied (backtracking).
6. Start the backtracking process by calling `backtrack` with the initial parameters.
7. Return the `result` list containing all the valid solutions.

# Complexity
- Time complexity: O(N!), where N is the size of the chessboard. In the worst case, the algorithm explores all possible configurations of placing N queens on an N x N chessboard.
- Space complexity: O(N) for the recursive call stack and the arrays used to keep track of occupied columns and diagonals.

# Code
```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }
        
        boolean[] cols = new boolean[n];
        boolean[] diag1 = new boolean[2 * n - 1]; // main diagonal: row - col + n - 1
        boolean[] diag2 = new boolean[2 * n - 1]; // anti-diagonal: row + col
        
        backtrack(0, n, board, cols, diag1, diag2, result);
        
        return result;
    }
    
    private void backtrack(int row, int n, char[][] board, boolean[] cols, boolean[] diag1, boolean[] diag2, List<List<String>> result) {
        if (row == n) {
            result.add(constructBoard(board));
            return;
        }
        
        for (int col = 0; col < n; col++) {
            if (!cols[col] && !diag1[row - col + n - 1] && !diag2[row + col]) {
                board[row][col] = 'Q';
                cols[col] = true;
                diag1[row - col + n - 1] = true;
                diag2[row + col] = true;
                
                backtrack(row + 1, n, board, cols, diag1, diag2, result);
                
                board[row][col] = '.';
                cols[col] = false;
                diag1[row - col + n - 1] = false;
                diag2[row + col] = false;
            }
        }
    }
    
    private List<String> constructBoard(char[][] board) {
        List<String> res = new ArrayList<>();
        for (char[] row : board) {
            res.add(new String(row));
        }
        return res;
    }
}
```