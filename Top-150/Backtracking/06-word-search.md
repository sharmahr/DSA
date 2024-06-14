[Word Search](https://leetcode.com/problems/word-search/description/)

# Intuition
The problem of determining if a word exists in a grid of characters can be solved using a backtracking approach. The intuition is to explore all possible paths in the grid by starting from each cell and recursively checking the neighboring cells to find a match for the given word. We can use a visited array to keep track of the cells that have been visited to avoid visiting the same cell multiple times.

# Approach
1. Initialize a boolean array `visited` of the same size as the `board` to keep track of visited cells.
2. Iterate through each cell in the `board`:
   - If the current cell matches the first character of the word, start the backtracking process from that cell.
   - If the backtracking process returns `true`, the word exists in the grid, so return `true`.
3. If the entire grid has been explored and the word is not found, return `false`.
4. Define a recursive function `backtrack` that takes the following parameters:
   - `board`: The grid of characters.
   - `word`: The word to be searched.
   - `index`: The current index of the word being matched.
   - `row`: The current row in the grid.
   - `col`: The current column in the grid.
   - `visited`: The boolean array to keep track of visited cells.
5. In the `backtrack` function:
   - Base case: If the index equals the length of the word, the entire word has been matched, so return `true`.
   - Check if the current cell is out of bounds, already visited, or the characters do not match. If any of these conditions are true, return `false`.
   - Mark the current cell as visited.
   - Recursively call `backtrack` on the neighboring cells (up, down, left, right) with the updated index.
   - If any of the recursive calls return `true`, the word exists in the grid, so return `true`.
   - Mark the current cell as unvisited (backtrack) to explore other paths.
   - Return `false` if none of the recursive calls return `true`.

# Complexity
- Time complexity: $O(m \times n \times 4^k)$, where $m$ is the number of rows, $n$ is the number of columns in the grid, and $k$ is the length of the word. In the worst case, for each cell, we explore all four directions, and the maximum depth of recursion is the length of the word.
- Space complexity: $O(m \times n)$ for the visited array and $O(k)$ for the recursive call stack, where $k$ is the length of the word.

# Code
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;

        boolean[][] visited = new boolean[m][n];
        for(int i=0; i < m; i++){
            for(int j=0; j< n; j++){
                if(backtrack(board, word, 0, i, j, visited)){
                    return true;
                }
            }
        }

        return false;
    }

    boolean backtrack(char[][] board, String word, int index, int row, int col, boolean[][] visited){
        if(index == word.length()){
            return true;
        }

        if(row < 0 || row >= board.length || col < 0 || col >= board[0].length || visited[row][col] || board[row][col] != word.charAt(index)){
            return false; //out of bounds, already visited or the characters do not match
        }

        visited[row][col] = true;

        boolean found = backtrack(board, word, index + 1, row - 1, col, visited)
                        || backtrack(board, word, index + 1, row + 1, col, visited)
                        || backtrack(board, word, index + 1, row, col - 1, visited)
                        || backtrack(board, word, index + 1, row, col + 1, visited);

        visited[row][col] = false;
        return found;
    }
}
```