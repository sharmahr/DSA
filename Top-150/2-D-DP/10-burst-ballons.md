[Burst Ballons](https://leetcode.com/problems/burst-balloons/)

# Intuition
The problem of bursting balloons to maximize the number of coins collected can be solved using dynamic programming. The intuition behind the solution is to consider the order in which the balloons are burst. We can divide the problem into smaller subproblems by considering the last balloon to be burst in each subproblem and recursively solve for the left and right subarrays.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `maxCoinsHelper(balloons, left, right)` that takes the array of balloons and the left and right boundaries of the current subproblem as parameters.
   - Base case: If `left > right`, return 0 since there are no balloons to burst.
   - Iterate over all possible balloons between `left` and `right` as the last balloon to burst.
   - For each balloon `i`, calculate the coins collected by bursting it last, which is `balloons[left-1] * balloons[i] * balloons[right+1]`.
   - Recursively solve for the left subarray (`left` to `i-1`) and the right subarray (`i+1` to `right`) and add their maximum coins to the current balloon's coins.
   - Return the maximum coins collected among all possible choices of the last balloon.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(n+2) × (n+2)` initialized with `-1` to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current subproblem is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a new array `balloons` of size `n+2` and add two additional balloons with value 1 at the beginning and end.
   - Create a 2D DP table `dp` of size `(n+2) × (n+2)` to store the maximum coins collected for each subproblem.
   - Iterate over all possible lengths of subarrays from 1 to n.
   - For each length `len`, iterate over all possible left boundaries `l` from 1 to `n-len+1`.
   - Calculate the corresponding right boundary `r` as `l+len-1`.
   - Iterate over all possible balloons between `l` and `r` as the last balloon to burst.
   - For each balloon `k`, calculate the coins collected by bursting it last, which is `balloons[l-1] * balloons[k] * balloons[r+1]`, and add the maximum coins collected from the left subarray (`dp[l][k-1]`) and the right subarray (`dp[k+1][r]`).
   - Update `dp[l][r]` with the maximum coins collected among all possible choices of the last balloon.
   - Return `dp[1][n]` as the maximum coins collected by bursting all balloons from index 1 to n.

# Complexity
- Time Complexity:
  - Recursive Approach: O(n!), where n is the number of balloons. The recursive function explores all possible permutations of bursting the balloons.
  - Memoized Approach: O(n^3), where n is the number of balloons. There are O(n^2) subproblems, and each subproblem takes O(n) time to solve.
  - Dynamic Programming Approach: O(n^3), where n is the number of balloons. The DP table has O(n^2) entries, and each entry takes O(n) time to fill.

- Space Complexity:
  - Recursive Approach: O(n) for the recursive call stack.
  - Memoized Approach: O(n^2) to store the memoization table.
  - Dynamic Programming Approach: O(n^2) to store the DP table.

# Recursive Approach
```java
class Solution {
    public int maxCoins(int[] nums) {
        int n = nums.length;
        int[] balloons = new int[n + 2];
        balloons[0] = 1;
        balloons[n + 1] = 1;
        for (int i = 0; i < n; i++) {
            balloons[i + 1] = nums[i];
        }
        
        return maxCoinsHelper(balloons, 1, n);
    }
    
    private int maxCoinsHelper(int[] balloons, int left, int right) {
        if (left > right) {
            return 0;
        }
        
        int maxCoins = 0;
        for (int i = left; i <= right; i++) {
            int coins = balloons[left - 1] * balloons[i] * balloons[right + 1];
            coins += maxCoinsHelper(balloons, left, i - 1) + maxCoinsHelper(balloons, i + 1, right);
            maxCoins = Math.max(maxCoins, coins);
        }
        
        return maxCoins;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int maxCoins(int[] nums) {
        int n = nums.length;
        int[] balloons = new int[n + 2];
        balloons[0] = 1;
        balloons[n + 1] = 1;
        for (int i = 0; i < n; i++) {
            balloons[i + 1] = nums[i];
        }
        
        int[][] memo = new int[n + 2][n + 2];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        
        return maxCoinsHelper(balloons, 1, n, memo);
    }
    
    private int maxCoinsHelper(int[] balloons, int left, int right, int[][] memo) {
        if (left > right) {
            return 0;
        }
        
        if (memo[left][right] != -1) {
            return memo[left][right];
        }
        
        int maxCoins = 0;
        for (int i = left; i <= right; i++) {
            int coins = balloons[left - 1] * balloons[i] * balloons[right + 1];
            coins += maxCoinsHelper(balloons, left, i - 1, memo) + maxCoinsHelper(balloons, i + 1, right, memo);
            maxCoins = Math.max(maxCoins, coins);
        }
        
        memo[left][right] = maxCoins;
        return maxCoins;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int maxCoins(int[] nums) {
        int n = nums.length;
        int[] balloons = new int[n + 2];
        balloons[0] = 1;
        balloons[n + 1] = 1;
        for (int i = 0; i < n; i++) {
            balloons[i + 1] = nums[i];
        }
        
        int[][] dp = new int[n + 2][n + 2];
        
        for (int len = 1; len <= n; len++) {
            for (int l = 1; l <= n - len + 1; l++) {
                int r = l + len - 1;
                for (int k = l; k <= r; k++) {
                    dp[l][r] = Math.max(dp[l][r], balloons[l - 1] * balloons[k] * balloons[r + 1] + dp[l][k - 1] + dp[k + 1][r]);
                }
            }
        }
        
        return dp[1][n];
    }
}
```