[Island And Treasure](https://neetcode.io/problems/islands-and-treasure)

# Intuition
To find the number of steps required to reach the nearest treasure chest for each land cell, we can perform a multi-source breadth-first search (BFS) starting from all the treasure chests. By using BFS, we can ensure that each land cell is visited in the shortest path from the nearest treasure chest.

# Approach
1. Initialize a queue to store the coordinates of the treasure chests.
2. Iterate through the grid and add the coordinates of all treasure chests (cells with value 0) to the queue.
3. Perform BFS starting from each treasure chest in the queue:
   - Dequeue a cell from the queue.
   - Explore the neighboring cells (up, down, left, right) of the current cell.
   - For each neighboring cell:
     - Check if the cell is within the grid bounds and is a land cell (represented by INF).
     - If the conditions are satisfied, update the value of the neighboring cell to the value of the current cell plus 1 (representing the number of steps from the nearest treasure chest).
     - Enqueue the neighboring cell to continue the BFS.
4. Repeat step 3 until the queue is empty.
5. After the BFS is complete, the grid will contain the number of steps required to reach the nearest treasure chest for each land cell.

# Complexity
- Time complexity: O(m * n)
  - The BFS will visit each cell in the grid at most once.
  - In the worst case, all cells are land cells, and the BFS will visit all cells.
  - Therefore, the time complexity is proportional to the number of cells in the grid.
- Space complexity: O(m * n)
  - In the worst case, if all cells are treasure chests, the queue will store all cells in the grid.
  - Therefore, the space complexity is proportional to the number of cells in the grid.

# Code
```java
class Solution {
    private static final int[][] DIRECTIONS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    private static final int INF = Integer.MAX_VALUE;

    public void islandsAndTreasure(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        Queue<int[]> queue = new ArrayDeque<>();

        // Add all treasure chests to the queue
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0) {
                    queue.offer(new int[]{i, j});
                }
            }
        }

        // BFS from each treasure chest
        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int row = cell[0];
            int col = cell[1];

            // Explore the neighboring cells
            for (int[] direction : DIRECTIONS) {
                int newRow = row + direction[0];
                int newCol = col + direction[1];

                // Check if the new cell is within the grid bounds and is a land cell
                if (newRow >= 0 && newRow < m && newCol >= 0 && newCol < n && grid[newRow][newCol] == INF) {
                    grid[newRow][newCol] = grid[row][col] + 1;
                    queue.offer(new int[]{newRow, newCol});
                }
            }
        }
    }
}
```