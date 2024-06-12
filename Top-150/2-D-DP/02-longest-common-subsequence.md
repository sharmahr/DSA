[Longest Increasing Subsequence](https://leetcode.com/problems/longest-common-subsequence/description/)

# Intuition
The problem of finding the length of the longest common subsequence (LCS) between two strings can be solved using dynamic programming. The intuition behind the solution is to build a 2D DP table where each cell represents the length of the LCS between the prefixes of the two strings up to the corresponding indices. We can fill the DP table in a bottom-up manner by considering the characters of both strings and making decisions based on whether they match or not.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `lcs(text1, text2, i, j)` that takes the two strings and their current indices as parameters.
   - Base case: If either `i` or `j` reaches the end of the string, return 0 since no common subsequence can be formed.
   - If the characters at indices `i` and `j` match, recursively call `lcs(text1, text2, i+1, j+1)` and add 1 to the result.
   - If the characters at indices `i` and `j` do not match, recursively call `lcs(text1, text2, i+1, j)` and `lcs(text1, text2, i, j+1)` and take the maximum of the two results.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(n+1) × (m+1)` initialized with -1.
   - Modify the recursive function to first check if the result for `(i, j)` is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 2D DP table `dp` of size `(n+1) × (m+1)` initialized with 0.
   - Initialize the base cases: `dp[0][j] = 0` and `dp[i][0] = 0` since an empty string has no common subsequence.
   - Iterate through the strings from index 1 to n and 1 to m.
   - For each pair of indices `(i, j)`, if the characters at `i-1` and `j-1` match, set `dp[i][j] = dp[i-1][j-1] + 1`.
   - If the characters do not match, set `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.
   - The length of the LCS will be stored in `dp[n][m]`.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(n+m)) in the worst case, where n and m are the lengths of the two strings. The recursive function explores all possible subsequences.
  - Memoized Approach: O(n*m) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(n*m) as we fill the DP table of size (n+1) × (m+1).

- Space Complexity:
  - Recursive Approach: O(max(n, m)) for the recursive call stack.
  - Memoized Approach: O(n*m) to store the memoization table.
  - Dynamic Programming Approach: O(n*m) to store the DP table.

# Recursive Approach
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        return lcs(text1, text2, 0, 0);
    }
    
    private int lcs(String text1, String text2, int i, int j) {
        if (i == text1.length() || j == text2.length()) {
            return 0;
        }
        
        if (text1.charAt(i) == text2.charAt(j)) {
            return 1 + lcs(text1, text2, i+1, j+1);
        } else {
            return Math.max(lcs(text1, text2, i+1, j), lcs(text1, text2, i, j+1));
        }
    }
}
```

# Memoized Approach
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n = text1.length();
        int m = text2.length();
        int[][] memo = new int[n][m];
        
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        
        return lcs(text1, text2, 0, 0, memo);
    }
    
    private int lcs(String text1, String text2, int i, int j, int[][] memo) {
        if (i == text1.length() || j == text2.length()) {
            return 0;
        }
        
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        
        if (text1.charAt(i) == text2.charAt(j)) {
            memo[i][j] = 1 + lcs(text1, text2, i+1, j+1, memo);
        } else {
            memo[i][j] = Math.max(lcs(text1, text2, i+1, j, memo), lcs(text1, text2, i, j+1, memo));
        }
        
        return memo[i][j];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n = text1.length();
        int m = text2.length();
        int[][] dp = new int[n+1][m+1];
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (text1.charAt(i-1) == text2.charAt(j-1)) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        
        return dp[n][m];
    }
}
```