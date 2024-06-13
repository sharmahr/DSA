[Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/description/)

# Intuition
The problem of matching a string with a regular expression containing '.' and '*' can be solved using dynamic programming. The intuition behind the solution is to consider each character of the string and the pattern one by one and make decisions based on whether they match or not. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `isMatchHelper(s, p, i, j)` that takes the string `s`, the pattern `p`, and their current indices `i` and `j` as parameters.
   - Base cases:
     - If both `i` and `j` reach the end of `s` and `p` respectively, return `true` since the string and pattern match.
     - If `j` reaches the end of `p` but `i` hasn't reached the end of `s`, return `false` since the pattern is exhausted but the string is not.
   - If the characters at indices `i` and `j` match (either the same character or '.' in the pattern), recursively call `isMatchHelper(s, p, i+1, j+1)`.
   - If the character at index `j+1` is '*', consider two cases:
     - Match 0 occurrences of the character before '*': Recursively call `isMatchHelper(s, p, i, j+2)`.
     - Match 1 or more occurrences of the character before '*': If the characters at indices `i` and `j` match (either the same character or '.' in the pattern), recursively call `isMatchHelper(s, p, i+1, j)`.
   - Return `false` if none of the above conditions are met.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(m+1) × (n+1)` initialized with `false`.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 2D DP table `dp` of size `(m+1) × (n+1)` to store the matching results.
   - Initialize `dp[0][0] = true` since an empty string matches an empty pattern.
   - Handle patterns like "a*", "a*b*", "a*b*c*" which can match an empty string by setting `dp[0][j] = dp[0][j-2]` if the character at index `j-1` is '*'.
   - Iterate through the characters of `s` and `p` simultaneously using two nested loops.
   - For each pair of indices `(i, j)`:
     - If the characters at `s[i-1]` and `p[j-1]` match (either the same character or '.' in the pattern), set `dp[i][j] = dp[i-1][j-1]`.
     - If the character at `p[j-1]` is '*', consider two cases:
       - Match 0 occurrences of the character before '*': Set `dp[i][j] = dp[i][j-2]`.
       - Match 1 or more occurrences of the character before '*': If the characters at `s[i-1]` and `p[j-2]` match (either the same character or '.' in the pattern), set `dp[i][j] = dp[i][j] || dp[i-1][j]`.
   - Return `dp[m][n]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(m+n)) in the worst case, where m and n are the lengths of `s` and `p` respectively. The recursive function explores all possible combinations of matching and not matching characters.
  - Memoized Approach: O(m*n) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(m*n) as we fill the `dp` table of size `(m+1) × (n+1)`.

- Space Complexity:
  - Recursive Approach: O(m+n) for the recursive call stack.
  - Memoized Approach: O(m*n) to store the memoization table.
  - Dynamic Programming Approach: O(m*n) to store the `dp` table.

# Recursive Approach
```java
class Solution {
    public boolean isMatch(String s, String p) {
        return isMatchHelper(s, p, 0, 0);
    }
    
    private boolean isMatchHelper(String s, String p, int i, int j) {
        if (i == s.length() && j == p.length()) {
            return true;
        }
        if (j == p.length()) {
            return false;
        }
        
        boolean match = (i < s.length() && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.'));
        
        if (j + 1 < p.length() && p.charAt(j + 1) == '*') {
            return isMatchHelper(s, p, i, j + 2) || (match && isMatchHelper(s, p, i + 1, j));
        }
        
        return match && isMatchHelper(s, p, i + 1, j + 1);
    }
}
```

# Memoized Approach
```java
class Solution {
    public boolean isMatch(String s, String p) {
        Boolean[][] memo = new Boolean[s.length() + 1][p.length() + 1];
        return isMatchHelper(s, p, 0, 0, memo);
    }
    
    private boolean isMatchHelper(String s, String p, int i, int j, Boolean[][] memo) {
        if (i == s.length() && j == p.length()) {
            return true;
        }
        if (j == p.length()) {
            return false;
        }
        
        if (memo[i][j] != null) {
            return memo[i][j];
        }
        
        boolean match = (i < s.length() && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '.'));
        
        if (j + 1 < p.length() && p.charAt(j + 1) == '*') {
            memo[i][j] = isMatchHelper(s, p, i, j + 2, memo) || (match && isMatchHelper(s, p, i + 1, j, memo));
        } else {
            memo[i][j] = match && isMatchHelper(s, p, i + 1, j + 1, memo);
        }
        
        return memo[i][j];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        
        for (int j = 2; j <= n; j++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 2];
            }
        }
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char sc = s.charAt(i - 1);
                char pc = p.charAt(j - 1);
                
                if (sc == pc || pc == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (pc == '*') {
                    dp[i][j] = dp[i][j - 2];
                    
                    char precedingChar = p.charAt(j - 2);
                    if (precedingChar == '.' || precedingChar == sc) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }
        
        return dp[m][n];
    }
}
```