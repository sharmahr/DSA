[Pacific Atlantic Waterflow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

# Intuition
To find the cells where water can flow to both the Pacific and Atlantic oceans, we can perform depth-first search (DFS) from the boundary cells of the matrix. We start the DFS from the top and left sides for the Pacific ocean and from the bottom and right sides for the Atlantic ocean. During the DFS, we mark the cells that can reach the respective ocean. Finally, we find the cells that are marked as reachable for both oceans.

# Approach
1. Initialize two boolean matrices, `pacific` and `atlantic`, to keep track of the cells that can reach the Pacific and Atlantic oceans, respectively.
2. Perform DFS from the top side of the matrix for the Pacific ocean.
3. Perform DFS from the left side of the matrix for the Pacific ocean.
4. Perform DFS from the bottom side of the matrix for the Atlantic ocean.
5. Perform DFS from the right side of the matrix for the Atlantic ocean.
6. During each DFS:
   - Check if the current cell is out of bounds, already visited, or has a height lower than the previous cell's height. If so, return.
   - Mark the current cell as visited in the respective boolean matrix.
   - Recursively perform DFS on the four adjacent cells (up, down, left, right) with the current cell's height as the previous height.
7. After the DFS traversals, iterate through the matrix and find the cells that are marked as reachable in both the `pacific` and `atlantic` matrices.
8. Add the coordinates of the cells that satisfy the condition to the result list.
9. Return the result list.

# Complexity
- Time complexity: O(rows * cols)
  - The DFS traversals visit each cell in the matrix at most once.
  - The iteration to find the cells reachable by both oceans also takes O(rows * cols) time.
  - Therefore, the overall time complexity is O(rows * cols).
- Space complexity: O(rows * cols)
  - The space complexity is determined by the two boolean matrices, `pacific` and `atlantic`, which store the reachability information for each cell.
  - The space required for the recursion stack in DFS is also proportional to the number of cells in the matrix.

# Code
```java
class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        int rows = heights.length, cols = heights[0].length;

        boolean[][] pacific = new boolean[rows][cols];
        boolean[][] atlantic = new boolean[rows][cols];

        // top side of the matrix
        for (int i = 0; i < cols; i++) {
            dfs(heights, pacific, 0, i, Integer.MIN_VALUE);
        }
        // left side of the matrix
        for (int i = 0; i < rows; i++) {
            dfs(heights, pacific, i, 0, Integer.MIN_VALUE);
        }
        // bottom side of the matrix
        for (int i = 0; i < cols; i++) {
            dfs(heights, atlantic, rows - 1, i, Integer.MIN_VALUE);
        }
        // right side of the matrix
        for (int i = 0; i < rows; i++) {
            dfs(heights, atlantic, i, cols - 1, Integer.MIN_VALUE);
        }

        List<List<Integer>> list = new ArrayList<>();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    list.add(Arrays.asList(i, j));
                }
            }
        }

        return list;
    }

    void dfs(int[][] heights, boolean[][] visited, int row, int col, int prevHeight) {
        if (row < 0 || row >= visited.length || col < 0 || col >= visited[0].length || visited[row][col] || heights[row][col] < prevHeight) {
            return;
        }
        visited[row][col] = true;
        dfs(heights, visited, row + 1, col, heights[row][col]);
        dfs(heights, visited, row - 1, col, heights[row][col]);
        dfs(heights, visited, row, col + 1, heights[row][col]);
        dfs(heights, visited, row, col - 1, heights[row][col]);
    }
}
```