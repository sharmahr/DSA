# Intuition
The problem asks to find all the cells in a matrix where water can flow to both the Pacific and Atlantic oceans. The intuition is to perform a depth-first search (DFS) from the boundary cells of the matrix and mark the cells that can reach the respective ocean. Then, find the cells that are marked as reachable to both oceans.

# Approach
1. Create two boolean matrices, `pacific` and `atlantic`, to mark the cells that can reach the Pacific and Atlantic oceans, respectively.
2. Perform DFS from the top and left boundaries of the matrix to mark the cells that can reach the Pacific ocean.
3. Perform DFS from the bottom and right boundaries of the matrix to mark the cells that can reach the Atlantic ocean.
4. In the DFS:
   - If the current cell is out of bounds, already visited, or the height of the current cell is less than the previous cell's height, return.
   - Mark the current cell as visited in the respective matrix.
   - Recursively explore the four adjacent cells (up, down, left, right) with the current cell's height as the new prevHeight.
5. Iterate through each cell in the matrix and add the coordinates of the cells that are marked as reachable to both oceans to the result list.
6. Return the result list containing the coordinates of the cells that can reach both oceans.

# Complexity
- Time complexity:
$$O(m \times n)$$, where m and n are the number of rows and columns in the matrix, respectively. Each cell is visited at most once during the DFS.

- Space complexity:
$$O(m \times n)$$ to store the `pacific` and `atlantic` matrices. The recursion stack can also go up to the size of the matrix in the worst case.

# Code
```java
class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        int rows = heights.length, cols = heights[0].length;
        
        boolean[][] pacific = new boolean[rows][cols];
        boolean[][] atlantic = new boolean[rows][cols];
        
        // DFS from top and left boundaries for Pacific ocean
        for (int i = 0; i < cols; i++) {
            dfs(heights, pacific, 0, i, Integer.MIN_VALUE);
        }
        for (int i = 0; i < rows; i++) {
            dfs(heights, pacific, i, 0, Integer.MIN_VALUE);
        }
        
        // DFS from bottom and right boundaries for Atlantic ocean
        for (int i = 0; i < cols; i++) {
            dfs(heights, atlantic, rows - 1, i, Integer.MIN_VALUE);
        }
        for (int i = 0; i < rows; i++) {
            dfs(heights, atlantic, i, cols - 1, Integer.MIN_VALUE);
        }
        
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.add(Arrays.asList(i, j));
                }
            }
        }
        
        return result;
    }
    
    private void dfs(int[][] heights, boolean[][] visited, int row, int col, int prevHeight) {
        if (row < 0 || row >= visited.length || col < 0 || col >= visited[0].length 
            || visited[row][col] || heights[row][col] < prevHeight) {
            return;
        }
        
        visited[row][col] = true;
        
        dfs(heights, visited, row - 1, col, heights[row][col]);  // Up
        dfs(heights, visited, row + 1, col, heights[row][col]);  // Down
        dfs(heights, visited, row, col - 1, heights[row][col]);  // Left
        dfs(heights, visited, row, col + 1, heights[row][col]);  // Right
    }
}
```