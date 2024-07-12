[Number of Islands](https://leetcode.com/problems/number-of-islands/)

# Intuition
The problem can be solved using a depth-first search (DFS) approach. We can traverse the grid and whenever we encounter a '1', we can perform DFS to explore the connected land cells and mark them as visited by changing them to '0'. Each DFS call will represent one island.

# Approach
1. Initialize a variable `count` to keep track of the number of islands.
2. Iterate through each cell in the grid using nested loops.
3. If the current cell is '1' (land), increment the `count` variable and perform DFS starting from the current cell.
4. In the DFS function:
   - Check if the current cell is within the grid boundaries and is a land cell ('1').
   - If the conditions are satisfied, mark the current cell as visited by changing it to '0'.
   - Recursively call DFS on the four adjacent cells (up, down, left, right).
5. After the nested loops complete, return the `count` variable as the number of islands.

# Complexity
- Time complexity: O(rows * cols)
  - The nested loops iterate through each cell in the grid once.
  - Each cell is visited at most once during the DFS traversal.
  - Therefore, the time complexity is proportional to the number of cells in the grid.
- Space complexity: O(rows * cols)
  - In the worst case, if the grid is filled with all land cells ('1'), the depth of the recursion in DFS can go up to `rows * cols`.
  - The space complexity is determined by the maximum depth of the recursion stack.

# Code
```java
class Solution {
    public int numIslands(char[][] grid) {
        // dfs and mark the visited items as '0'
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
        grid[row][col] = '0';
        dfs(grid, row - 1, col);  // Up
        dfs(grid, row + 1, col);  // Down
        dfs(grid, row, col + 1);  // Right
        dfs(grid, row, col - 1);  // Left
    }
}
```