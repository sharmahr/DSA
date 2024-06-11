[Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

# Intuition
To determine the minimum number of minutes required for all oranges to rot, we can use a breadth-first search (BFS) approach. We start with the initially rotten oranges and spread the rot to their adjacent fresh oranges in each minute. We continue this process until all fresh oranges have rotted or there are no more rotten oranges to spread the rot.

# Approach
1. Initialize a queue to store the positions of rotten oranges and a variable `freshCount` to keep track of the count of fresh oranges.
2. Iterate through the grid and add the positions of rotten oranges to the queue. Also, increment `freshCount` for each fresh orange encountered.
3. If there are no fresh oranges (`freshCount` is 0), return 0 as all oranges are already rotten.
4. Initialize a variable `min` to keep track of the minimum number of minutes.
5. While the queue is not empty, do the following:
   - Get the size of the queue, which represents the number of rotten oranges at the current level.
   - Initialize a boolean variable `hasRotten` to track if any fresh orange has rotted at the current level.
   - Iterate through the current level of rotten oranges:
     - Dequeue an orange from the queue and get its position.
     - Explore the four adjacent cells (up, down, left, right) of the current orange.
     - If an adjacent cell is within the grid bounds and contains a fresh orange (value 1):
       - Mark the fresh orange as rotten (value 2) and add its position to the queue.
       - Decrement `freshCount` as a fresh orange has rotted.
       - Set `hasRotten` to true to indicate that a fresh orange has rotted at the current level.
   - If `hasRotten` is true, increment `min` as a minute has passed.
6. After the BFS traversal, if `freshCount` is 0, return `min` as all oranges have rotted. Otherwise, return -1 as there are still fresh oranges remaining.

# Complexity
- Time complexity: O(rows * cols)
  - The BFS traversal visits each cell in the grid at most once.
  - In the worst case, all cells contain fresh oranges, and the BFS traversal needs to visit all cells.
- Space complexity: O(rows * cols)
  - In the worst case, if all oranges are rotten initially, the queue may contain all cells in the grid.

# Code
```java
class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        Queue<int[]> queue = new LinkedList<>();
        int freshCount = 0; // keep track of the fresh count

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    freshCount += 1;
                }
            }
        }

        if (freshCount == 0) return 0;

        int min = 0;
        int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

        while (!queue.isEmpty()) {
            int size = queue.size();
            boolean hasRotten = false;

            for (int i = 0; i < size; i++) {
                int[] orange = queue.poll();
                int x = orange[0];
                int y = orange[1];

                for (int[] dir : directions) {
                    int newX = x + dir[0];
                    int newY = y + dir[1];

                    if (newX >= 0 && newX < rows && newY >= 0 && newY < cols && grid[newX][newY] == 1) {
                        grid[newX][newY] = 2; // rot the orange
                        queue.offer(new int[]{newX, newY});
                        freshCount -= 1;
                        hasRotten = true;
                    }
                }
            }

            if (hasRotten) {
                min += 1;
            }
        }

        return freshCount == 0 ? min : -1;
    }
}
```