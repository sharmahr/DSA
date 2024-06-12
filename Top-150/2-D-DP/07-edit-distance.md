[Edit Distance](https://leetcode.com/problems/edit-distance/description/)

# Intuition
The problem of finding the minimum number of operations (insert, delete, replace) to convert one string into another can be solved using dynamic programming. The intuition behind the solution is to consider the characters of both strings one by one and make decisions based on whether they match or not. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `minDistanceHelper(word1, word2, i, j)` that takes the two strings and their current indices `i` and `j` as parameters.
   - Base cases:
     - If `i` reaches the end of `word1`, return the remaining length of `word2` (i.e., `n - j`) as we need to perform insertions for the remaining characters.
     - If `j` reaches the end of `word2`, return the remaining length of `word1` (i.e., `m - i`) as we need to perform deletions for the remaining characters.
   - If the characters at indices `i` and `j` match, recursively call `minDistanceHelper(word1, word2, i + 1, j + 1)` without any operation.
   - If the characters at indices `i` and `j` do not match, consider three options:
     - Insert a character: Recursively call `minDistanceHelper(word1, word2, i, j + 1)` and add 1 to the result.
     - Delete a character: Recursively call `minDistanceHelper(word1, word2, i + 1, j)` and add 1 to the result.
     - Replace a character: Recursively call `minDistanceHelper(word1, word2, i + 1, j + 1)` and add 1 to the result.
   - Return the minimum value among the three options.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(m + 1) × (n + 1)` initialized with `-1` to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 2D DP table `dp` of size `(m + 1) × (n + 1)` to store the minimum number of operations required to convert the substrings.
   - Initialize the base cases:
     - `dp[i][0] = i` for all `i` from `0` to `m`, as we need `i` deletions to convert `word1[:i]` to an empty string.
     - `dp[0][j] = j` for all `j` from `0` to `n`, as we need `j` insertions to convert an empty string to `word2[:j]`.
   - Iterate through the characters of `word1` and `word2` simultaneously using two nested loops.
   - For each pair of indices `(i, j)`, if the characters at `i-1` and `j-1` match, set `dp[i][j] = dp[i-1][j-1]` as no operation is required.
   - If the characters do not match, set `dp[i][j]` to the minimum value among three options:
     - Insert a character: `dp[i][j-1] + 1`
     - Delete a character: `dp[i-1][j] + 1`
     - Replace a character: `dp[i-1][j-1] + 1`
   - Return `dp[m][n]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(3^(m+n)) in the worst case, where m and n are the lengths of `word1` and `word2` respectively. The recursive function explores all possible operations at each step.
  - Memoized Approach: O(m*n) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(m*n) as we fill the `dp` table of size `(m+1) × (n+1)`.

- Space Complexity:
  - Recursive Approach: O(m+n) for the recursive call stack.
  - Memoized Approach: O(m*n) to store the memoization table.
  - Dynamic Programming Approach: O(m*n) to store the `dp` table.

# Recursive Approach
```java
class Solution {
    public int minDistance(String word1, String word2) {
        return minDistanceHelper(word1, word2, 0, 0);
    }
    
    private int minDistanceHelper(String word1, String word2, int i, int j) {
        if (i == word1.length()) {
            return word2.length() - j;
        }
        if (j == word2.length()) {
            return word1.length() - i;
        }
        
        if (word1.charAt(i) == word2.charAt(j)) {
            return minDistanceHelper(word1, word2, i + 1, j + 1);
        } else {
            int insert = minDistanceHelper(word1, word2, i, j + 1) + 1;
            int delete = minDistanceHelper(word1, word2, i + 1, j) + 1;
            int replace = minDistanceHelper(word1, word2, i + 1, j + 1) + 1;
            return Math.min(insert, Math.min(delete, replace));
        }
    }
}
```

# Memoized Approach
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] memo = new int[m + 1][n + 1];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return minDistanceHelper(word1, word2, 0, 0, memo);
    }
    
    private int minDistanceHelper(String word1, String word2, int i, int j, int[][] memo) {
        if (i == word1.length()) {
            return word2.length() - j;
        }
        if (j == word2.length()) {
            return word1.length() - i;
        }
        
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        
        if (word1.charAt(i) == word2.charAt(j)) {
            memo[i][j] = minDistanceHelper(word1, word2, i + 1, j + 1, memo);
        } else {
            int insert = minDistanceHelper(word1, word2, i, j + 1, memo) + 1;
            int delete = minDistanceHelper(word1, word2, i + 1, j, memo) + 1;
            int replace = minDistanceHelper(word1, word2, i + 1, j + 1, memo) + 1;
            memo[i][j] = Math.min(insert, Math.min(delete, replace));
        }
        
        return memo[i][j];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i][j - 1], Math.min(dp[i - 1][j], dp[i - 1][j - 1])) + 1;
                }
            }
        }
        
        return dp[m][n];
    }
}
```