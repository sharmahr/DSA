[Distinct Subsequence](https://leetcode.com/problems/distinct-subsequences/description/)

# Intuition
The problem of finding the number of distinct subsequences of a string `t` in another string `s` can be solved using dynamic programming. The intuition behind the solution is to consider each character of `s` and `t` one by one and make decisions based on whether they match or not. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `numDistinctHelper(s, t, i, j)` that takes the two strings and their current indices `i` and `j` as parameters.
   - Base cases:
     - If `j` reaches the end of `t`, it means we have found a valid subsequence, so return 1.
     - If `i` reaches the end of `s` but `j` hasn't reached the end of `t`, it means we cannot form a valid subsequence, so return 0.
   - If the characters at indices `i` and `j` match, we have two choices:
     - Include the current character and recursively call `numDistinctHelper(s, t, i + 1, j + 1)`.
     - Exclude the current character and recursively call `numDistinctHelper(s, t, i + 1, j)`.
   - If the characters at indices `i` and `j` do not match, we can only exclude the current character of `s` and recursively call `numDistinctHelper(s, t, i + 1, j)`.
   - Return the sum of the results obtained from the recursive calls.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(m + 1) × (n + 1)` initialized with `-1` to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 2D DP table `dp` of size `(m + 1) × (n + 1)` to store the number of distinct subsequences.
   - Initialize the base cases:
     - `dp[0][0] = 1` because an empty string is considered a valid subsequence of an empty string.
     - `dp[i][0] = 1` for all `i` from `1` to `m` because there is exactly one way to form an empty subsequence from any substring of `s` (by not including any characters).
   - Iterate through the characters of `s` and `t` simultaneously using two nested loops.
   - For each pair of indices `(i, j)`:
     - If the characters at `s[i-1]` and `t[j-1]` match, update `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]`.
     - If the characters do not match, update `dp[i][j] = dp[i-1][j]`.
   - Return `dp[m][n]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(m+n)) in the worst case, where m and n are the lengths of `s` and `t` respectively. The recursive function explores all possible combinations of including or excluding characters.
  - Memoized Approach: O(m*n) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(m*n) as we fill the `dp` table of size `(m+1) × (n+1)`.

- Space Complexity:
  - Recursive Approach: O(m+n) for the recursive call stack.
  - Memoized Approach: O(m*n) to store the memoization table.
  - Dynamic Programming Approach: O(m*n) to store the `dp` table.

# Recursive Approach
```java
class Solution {
    public int numDistinct(String s, String t) {
        return numDistinctHelper(s, t, 0, 0);
    }
    
    private int numDistinctHelper(String s, String t, int i, int j) {
        if (j == t.length()) {
            return 1;
        }
        if (i == s.length()) {
            return 0;
        }
        
        int count = 0;
        if (s.charAt(i) == t.charAt(j)) {
            count += numDistinctHelper(s, t, i + 1, j + 1);
        }
        count += numDistinctHelper(s, t, i + 1, j);
        
        return count;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[][] memo = new int[m + 1][n + 1];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return numDistinctHelper(s, t, 0, 0, memo);
    }
    
    private int numDistinctHelper(String s, String t, int i, int j, int[][] memo) {
        if (j == t.length()) {
            return 1;
        }
        if (i == s.length()) {
            return 0;
        }
        
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        
        int count = 0;
        if (s.charAt(i) == t.charAt(j)) {
            count += numDistinctHelper(s, t, i + 1, j + 1, memo);
        }
        count += numDistinctHelper(s, t, i + 1, j, memo);
        
        memo[i][j] = count;
        return count;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[][] dp = new int[m + 1][n + 1];
        
        // Base case: dp[0][0] = 1 (empty string is a subsequence of empty string)
        dp[0][0] = 1;
        
        // Initialize dp[i][0] to 1 (empty string is a subsequence of any string)
        for (int i = 1; i <= m; i++) {
            dp[i][0] = 1;
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
                } else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        
        return dp[m][n];
    }
}
```