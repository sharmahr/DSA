[Max Area of Islands](https://leetcode.com/problems/max-area-of-island/description/)

# Intuition
To find the maximum area of an island, we can use a depth-first search (DFS) approach. We can traverse the grid and whenever we encounter a cell with value 1 (representing land), we perform DFS to explore the connected land cells and count the area of that island. We keep track of the maximum area encountered during the traversal.

# Approach
1. Initialize a variable `max` to keep track of the maximum area of an island.
2. Iterate through each cell in the grid using nested loops.
3. If the current cell is 1 (land), perform DFS starting from the current cell and update `max` with the maximum value between the current `max` and the area returned by the DFS.
4. In the DFS function:
   - Check if the current cell is within the grid boundaries and is a land cell (1).
   - If the conditions are not satisfied, return 0 as the area.
   - Mark the current cell as visited by changing it to 0.
   - Initialize a variable `count` to 1 to count the current cell.
   - Recursively call DFS on the four adjacent cells (up, down, left, right) and add their returned areas to `count`.
   - Return the total `count` as the area of the connected island.
5. After the nested loops complete, return the `max` variable as the maximum area of an island.

# Complexity
- Time complexity: O(rows * cols)
  - The nested loops iterate through each cell in the grid once.
  - Each cell is visited at most once during the DFS traversal.
  - Therefore, the time complexity is proportional to the number of cells in the grid.
- Space complexity: O(rows * cols)
  - In the worst case, if the grid is filled with all land cells (1), the depth of the recursion in DFS can go up to `rows * cols`.
  - The space complexity is determined by the maximum depth of the recursion stack.

# Code
```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int rows = grid.length, cols = grid[0].length;
        int max = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 1) {
                    max = Math.max(dfs(grid, i, j), max);
                }
            }
        }
        return max;
    }

    private int dfs(int[][] grid, int row, int col) {
        if (row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] == 0) {
            return 0;
        }
        grid[row][col] = 0;
        int count = 1;
        count += dfs(grid, row + 1, col);  // Down
        count += dfs(grid, row - 1, col);  // Up
        count += dfs(grid, row, col + 1);  // Right
        count += dfs(grid, row, col - 1);  // Left
        return count;
    }
}
```