[Swim In rising Water](https://leetcode.com/problems/swim-in-rising-water/)

# Intuition
To find the minimum time required to swim from the top-left corner to the bottom-right corner, we can use Dijkstra's algorithm. We can treat each cell in the grid as a node in a graph, and the value of each cell represents the time required to swim through that cell. We can use a priority queue (min-heap) to always select the cell with the minimum time.

# Approach
1. Check if the grid has only one cell. If so, return 0 as the minimum time.
2. Create a boolean array `visited` to keep track of visited cells.
3. Create a priority queue (min-heap) to store the cells as `[height, row, col]` tuples, where `height` represents the time required to swim through that cell.
4. Add the top-left cell `[grid[0][0], 0, 0]` to the priority queue.
5. Initialize a variable `result` to store the maximum time encountered so far.
6. While the priority queue is not empty:
   - Remove the cell with the minimum time from the priority queue.
   - Update `result` with the maximum value between `result` and the time of the current cell.
   - If the current cell is the bottom-right cell, break the loop as we have reached the destination.
   - Explore the four adjacent cells (up, down, left, right) of the current cell:
     - Check if the adjacent cell is within the grid boundaries and has not been visited.
     - If the conditions are satisfied, add the adjacent cell to the priority queue with its corresponding time and mark it as visited.
7. Return `result` as the minimum time required to swim from the top-left corner to the bottom-right corner.

# Complexity
- Time complexity: O(N^2 * log(N^2))
  - N is the length of the grid (assuming it is a square grid).
  - In the worst case, all cells will be visited, and for each cell, we add its adjacent cells to the priority queue.
  - Adding an element to the priority queue takes O(log(N^2)) time, and we perform this operation for each cell.
- Space complexity: O(N^2)
  - The priority queue can store at most all the cells in the grid, which is N^2 cells.
  - The `visited` array also requires O(N^2) space to store the visited status of each cell.

# Code
```java
class Solution {
    int[][] directions = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

    public int swimInWater(int[][] grid) {
        int length = grid.length;
        if (length == 1) return 0; // base case

        boolean[][] visited = new boolean[length][length];
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[0] - b[0]);

        heap.add(new int[]{grid[0][0], 0, 0}); // insert into the heap as [height, row, col]
        int result = 0;

        while (!heap.isEmpty()) {
            int[] current = heap.poll();
            result = Math.max(result, current[0]);

            if (current[1] == length - 1 && current[2] == length - 1) {
                break;
            }

            for (int[] direction : directions) {
                int x = current[1] + direction[0];
                int y = current[2] + direction[1];

                if (x < 0 || x >= length || y < 0 || y >= length || visited[x][y]) {
                    continue;
                }

                heap.add(new int[]{grid[x][y], x, y});
                visited[x][y] = true;
            }
        }

        return result;
    }
}
```