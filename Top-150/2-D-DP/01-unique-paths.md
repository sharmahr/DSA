[Unique Paths](https://leetcode.com/problems/unique-paths/)

# Intuition
The problem of finding the number of unique paths from the top-left corner to the bottom-right corner of a grid can be solved using dynamic programming. The intuition behind the solution is that the number of unique paths to reach any cell in the grid is the sum of the number of unique paths from the cell above it and the cell to its left. We can build a 2D array to store the number of unique paths for each cell and fill it in a bottom-up manner.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the number of unique paths by defining a function that takes the current position (row and column) as parameters. The base cases are when we reach the bottom-right corner (return 1) or when we go out of bounds (return 0). For each cell, we recursively calculate the number of unique paths by summing the paths from the cell below it and the cell to its right.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use a 2D array to store the number of unique paths for each cell and retrieve them when needed.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to solve this problem efficiently. We use a 2D array `dp` where `dp[i][j]` represents the number of unique paths from the top-left corner to the cell `(i, j)`. We initialize the first row and first column of `dp` with 1 since there is only one way to reach those cells. Then, we fill the `dp` array using the formula: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`, which means the number of unique paths to reach cell `(i, j)` is the sum of the paths from the cell above it and the cell to its left.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(m+n)), where m and n are the dimensions of the grid. In the worst case, we explore all possible paths, which is exponential.
  - Memoized Approach: O(m*n), where m and n are the dimensions of the grid. We solve each subproblem once and store the result, reducing the time complexity to the number of cells in the grid.
  - Dynamic Programming Approach: O(m*n), where m and n are the dimensions of the grid. We fill the `dp` array once for each cell.

- Space Complexity:
  - Recursive Approach: O(m+n) to store the recursive call stack.
  - Memoized Approach: O(m*n) to store the memoization array.
  - Dynamic Programming Approach: O(m*n) to store the `dp` array. However, we can optimize it to O(n) by using a 1D array instead of a 2D array since we only need the previous row's values.

# Recursive Approach
```java
class Solution {
    public int uniquePaths(int m, int n) {
        return uniquePathsHelper(0, 0, m, n);
    }
    
    private int uniquePathsHelper(int row, int col, int m, int n) {
        if (row == m - 1 && col == n - 1) {
            return 1;
        }
        
        if (row >= m || col >= n) {
            return 0;
        }
        
        int pathsDown = uniquePathsHelper(row + 1, col, m, n);
        int pathsRight = uniquePathsHelper(row, col + 1, m, n);
        
        return pathsDown + pathsRight;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] memo = new int[m][n];
        return uniquePathsHelper(0, 0, m, n, memo);
    }
    
    private int uniquePathsHelper(int row, int col, int m, int n, int[][] memo) {
        if (row == m - 1 && col == n - 1) {
            return 1;
        }
        
        if (row >= m || col >= n) {
            return 0;
        }
        
        if (memo[row][col] != 0) {
            return memo[row][col];
        }
        
        int pathsDown = uniquePathsHelper(row + 1, col, m, n, memo);
        int pathsRight = uniquePathsHelper(row, col + 1, m, n, memo);
        
        memo[row][col] = pathsDown + pathsRight;
        return memo[row][col];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        
        // Initialize the first row and first column with 1
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }
        
        // Fill the dp array
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        
        return dp[m-1][n-1];
    }
}
```