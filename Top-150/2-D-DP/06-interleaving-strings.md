[Interleaving Strings](https://leetcode.com/problems/interleaving-string/description/)

# Intuition
The problem of determining whether a string `s3` is formed by interleaving strings `s1` and `s2` can be solved using dynamic programming. The intuition behind the solution is to consider the characters of `s1` and `s2` one by one and check if they match the characters of `s3` in a valid interleaving order. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `isInterleaveHelper(s1, s2, s3, i, j, k)` that takes the three strings and their current indices `i`, `j`, and `k` as parameters.
   - Base cases:
     - If the index `k` reaches the end of `s3` and both `i` and `j` reach the end of `s1` and `s2` respectively, return `true` since we have found a valid interleaving.
     - If the index `k` reaches the end of `s3` but either `i` or `j` has not reached the end of `s1` or `s2`, return `false` since it is an invalid interleaving.
   - Recursive calls:
     - If the character at index `i` of `s1` matches the character at index `k` of `s3`, recursively call `isInterleaveHelper(s1, s2, s3, i + 1, j, k + 1)`.
     - If the character at index `j` of `s2` matches the character at index `k` of `s3`, recursively call `isInterleaveHelper(s1, s2, s3, i, j + 1, k + 1)`.
   - Return the logical OR of the results from the recursive calls.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(length of s1 + 1) × (length of s2 + 1)` initialized with `null` to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 2D DP table `dp` of size `(length of s1 + 1) × (length of s2 + 1)` initialized with `false`.
   - Initialize `dp[0][0] = true` since an empty string is considered a valid interleaving of two empty strings.
   - Iterate through the characters of `s1` and `s2` simultaneously.
   - For each pair of indices `(i, j)`, update `dp[i][j]` as follows:
     - If the character at index `i-1` of `s1` matches the character at index `i+j-1` of `s3`, set `dp[i][j] = dp[i][j] || dp[i-1][j]`.
     - If the character at index `j-1` of `s2` matches the character at index `i+j-1` of `s3`, set `dp[i][j] = dp[i][j] || dp[i][j-1]`.
   - Return `dp[length of s1][length of s2]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(m+n)) in the worst case, where m and n are the lengths of `s1` and `s2` respectively. The recursive function explores all possible interleaving combinations.
  - Memoized Approach: O(m*n) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(m*n) as we fill the `dp` table of size `(m+1) × (n+1)`.

- Space Complexity:
  - Recursive Approach: O(m+n) for the recursive call stack.
  - Memoized Approach: O(m*n) to store the memoization table.
  - Dynamic Programming Approach: O(m*n) to store the `dp` table.

# Recursive Approach
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) {
            return false;
        }
        return isInterleaveHelper(s1, s2, s3, 0, 0, 0);
    }
    
    private boolean isInterleaveHelper(String s1, String s2, String s3, int i, int j, int k) {
        if (k == s3.length()) {
            return true;
        }
        
        boolean takeS1 = i < s1.length() && s1.charAt(i) == s3.charAt(k) && isInterleaveHelper(s1, s2, s3, i + 1, j, k + 1);
        boolean takeS2 = j < s2.length() && s2.charAt(j) == s3.charAt(k) && isInterleaveHelper(s1, s2, s3, i, j + 1, k + 1);
        
        return takeS1 || takeS2;
    }
}
```

# Memoized Approach
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length();
        int len2 = s2.length();
        int len3 = s3.length();
        
        if (len1 + len2 != len3) {
            return false;
        }
        
        Boolean[][] memo = new Boolean[len1 + 1][len2 + 1];
        return isInterleaveHelper(s1, s2, s3, 0, 0, 0, memo);
    }
    
    private boolean isInterleaveHelper(String s1, String s2, String s3, int i, int j, int k, Boolean[][] memo) {
        if (k == s3.length()) {
            return true;
        }
        
        if (memo[i][j] != null) {
            return memo[i][j];
        }
        
        boolean takeS1 = i < s1.length() && s1.charAt(i) == s3.charAt(k) && isInterleaveHelper(s1, s2, s3, i + 1, j, k + 1, memo);
        boolean takeS2 = j < s2.length() && s2.charAt(j) == s3.charAt(k) && isInterleaveHelper(s1, s2, s3, i, j + 1, k + 1, memo);
        
        memo[i][j] = takeS1 || takeS2;
        return memo[i][j];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length();
        int len2 = s2.length();
        int len3 = s3.length();
        
        if (len1 + len2 != len3) {
            return false;
        }
        
        boolean[][] dp = new boolean[len1 + 1][len2 + 1];
        dp[0][0] = true;
        
        for (int i = 1; i <= len1; i++) {
            dp[i][0] = dp[i - 1][0] && s1.charAt(i - 1) == s3.charAt(i - 1);
        }
        
        for (int j = 1; j <= len2; j++) {
            dp[0][j] = dp[0][j - 1] && s2.charAt(j - 1) == s3.charAt(j - 1);
        }
        
        for (int i = 1; i <= len1; i++) {
            for (int j = 1; j <= len2; j++) {
                dp[i][j] = (dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) ||
                           (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
            }
        }
        
        return dp[len1][len2];
    }
}
```