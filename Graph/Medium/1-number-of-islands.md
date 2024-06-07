[Problem Statement](https://leetcode.com/problems/number-of-islands/description/)

# Intuition
The problem asks to find the number of islands in a 2D grid. An island is a group of connected '1's (land) surrounded by '0's (water) or the grid boundaries. The intuition is to perform a depth-first search (DFS) starting from each unvisited '1' cell and mark all the connected '1' cells as visited. The number of times the DFS is initiated will give the count of islands.

# Approach
1. Initialize a variable `count` to keep track of the number of islands.
2. Iterate through each cell in the grid.
3. If the current cell is '1' (land), increment the `count` and perform a DFS starting from that cell.
4. In the DFS:
   - Mark the current cell as visited by changing its value to '0'.
   - Recursively explore the four adjacent cells (up, down, left, right) if they are within the grid boundaries and are '1' (land).
5. Return the `count` as the number of islands.

# Complexity
- Time complexity:
$$O(m \times n)$$, where m and n are the number of rows and columns in the grid, respectively. Each cell is visited at most once during the DFS.

- Space complexity:
$$O(m \times n)$$ in the worst case, where the entire grid is filled with '1's. The recursion stack can go up to the size of the grid.

# Code
```java
class Solution {
    public int numIslands(char[][] grid) {
        int count = 0;
        int rows = grid.length, cols = grid[0].length;
        
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == '1') {
                    count++;
                    dfs(grid, i, j);
                }
            }
        }
        
        return count;
    }
    
    private void dfs(char[][] grid, int row, int col) {
        if (row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] != '1') {
            return;
        }
        
        grid[row][col] = '0';  // Mark the current cell as visited
        
        // Explore the four adjacent cells
        dfs(grid, row - 1, col);  // Up
        dfs(grid, row + 1, col);  // Down
        dfs(grid, row, col - 1);  // Left
        dfs(grid, row, col + 1);  // Right
    }
}
```

The code iterates through each cell in the grid. When it encounters a '1' cell, it increments the `count` and performs a DFS starting from that cell. The DFS marks the current cell as visited by changing its value to '0' and recursively explores the four adjacent cells. This process continues until all connected '1' cells are visited. Finally, the code returns the `count` as the number of islands.