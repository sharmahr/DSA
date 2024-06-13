[Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/description/)

# Intuition
The problem of finding the longest increasing path in a matrix can be solved using dynamic programming and depth-first search (DFS). The intuition behind the solution is to explore all possible paths starting from each cell in the matrix and keep track of the longest increasing path found so far. We can use memoization to avoid redundant calculations and optimize the solution.

# Approach
We can solve this problem using a combination of DFS and dynamic programming:

1. Create a 2D array `dp` of the same size as the input matrix to store the lengths of the longest increasing paths starting from each cell.

2. Traverse each cell in the matrix and perform the following steps:
   - If the longest increasing path starting from the current cell is already computed and stored in `dp`, return that value.
   - Initialize a variable `maxPath` to 1 to represent the minimum path length.
   - Explore all four adjacent cells (up, down, left, right) and check if they are within the matrix bounds and have a value greater than the current cell.
   - If an adjacent cell satisfies the conditions, recursively compute the longest increasing path starting from that cell by calling the `dfs` function.
   - Update `maxPath` by taking the maximum value among the current `maxPath` and the longest increasing path returned by the recursive calls plus 1.
   - Store the computed `maxPath` value in `dp` for the current cell and return it.

3. Initialize a variable `maxPath` to 1 to store the overall maximum path length.

4. Traverse each cell in the matrix and call the `dfs` function to compute the longest increasing path starting from that cell.

5. Update `maxPath` by taking the maximum value among the current `maxPath` and the longest increasing path returned by the `dfs` function.

6. Return the final value of `maxPath` as the result.

# Complexity
- Time Complexity: O(m * n), where m is the number of rows and n is the number of columns in the matrix. Each cell is visited at most once, and the DFS function takes constant time for each cell.
- Space Complexity: O(m * n) to store the memoization table `dp`. In the worst case, the recursive call stack may also reach a depth of O(m * n) if the matrix forms a single increasing path.

# Recursive Approach
```java
class Solution {
    private int[][] directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        
        int m = matrix.length;
        int n = matrix[0].length;
        int maxPath = 1;
        
        // Traverse each cell and compute longest path starting from that cell
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maxPath = Math.max(maxPath, dfs(matrix, i, j, -1));
            }
        }
        
        return maxPath;
    }
    
    private int dfs(int[][] matrix, int i, int j, int prevVal) {
        if (i < 0 || i >= matrix.length || j < 0 || j >= matrix[0].length || matrix[i][j] <= prevVal) {
            return 0;
        }
        
        int maxPath = 1;
        
        for (int[] dir : directions) {
            int x = i + dir[0];
            int y = j + dir[1];
            maxPath = Math.max(maxPath, 1 + dfs(matrix, x, y, matrix[i][j]));
        }
        
        return maxPath;
    }
}
```

# Memoized Approach
```java
class Solution {
    private int[][] directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    
    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] dp = new int[m][n];
        int maxPath = 1;
        
        // Traverse each cell and compute longest path starting from that cell
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maxPath = Math.max(maxPath, dfs(matrix, dp, i, j));
            }
        }
        
        return maxPath;
    }
    
    private int dfs(int[][] matrix, int[][] dp, int i, int j) {
        if (dp[i][j] != 0) {
            return dp[i][j];
        }
        
        int maxPath = 1;
        
        for (int[] dir : directions) {
            int x = i + dir[0];
            int y = j + dir[1];
            
            if (x >= 0 && x < matrix.length && y >= 0 && y < matrix[0].length && matrix[x][y] > matrix[i][j]) {
                maxPath = Math.max(maxPath, 1 + dfs(matrix, dp, x, y));
            }
        }
        
        dp[i][j] = maxPath;
        return maxPath;
    }
}
```

The memoized approach is an optimization of the recursive approach. We use a 2D array `dp` to store the computed longest increasing path lengths for each cell. Before making a recursive call, we check if the result for the current cell is already computed and stored in `dp`. If it is, we return that value instead of recomputing it. This helps avoid redundant calculations and reduces the time complexity.

# Dynamic Programming Approach
The dynamic programming approach is already implemented in the memoized approach. The memoization table `dp` serves as the DP table, and the `dfs` function fills the table in a top-down manner. The final result is the maximum value in the `dp` table.

The code you provided is an example of the memoized approach, which is a form of dynamic programming. The `dp` array is used to store the computed results and avoid redundant calculations.