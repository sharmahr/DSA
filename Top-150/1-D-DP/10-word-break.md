[Word break](https://leetcode.com/problems/word-break/)

# Intuition
The problem of word break can be solved using dynamic programming. The intuition behind the solution is to determine if the given string can be segmented into a space-separated sequence of one or more dictionary words. We can solve this problem by considering subproblems and using the results of smaller subproblems to solve larger ones.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively check if the given string can be segmented into dictionary words. We start from the beginning of the string and try to find a valid word from the dictionary. If a valid word is found, we recursively check if the remaining substring can be segmented. If we reach the end of the string, it means the string can be segmented into dictionary words.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use a boolean array to store the results of subproblems and retrieve them when needed.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to solve this problem. We use a boolean array `dp` where `dp[i]` represents whether the substring from index 0 to i-1 can be segmented into dictionary words. We start from the end of the string and fill the `dp` array. For each index i, we check if the substring starting from i can form a valid word and if the remaining substring (from index i + word.length() to the end) can be segmented.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the length of the string. In the worst case, we have 2^n possible substrings to check.
  - Memoized Approach: $$O(n^2)$$, where n is the length of the string. We have n subproblems, and for each subproblem, we iterate through the dictionary words, which can take up to n time.
  - Dynamic Programming Approach: $$O(n^2)$$, where n is the length of the string. We fill the `dp` array of size n+1, and for each index, we iterate through the dictionary words, which can take up to n time.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(n)$$ to store the `dp` array.

# Recursive Approach
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return wordBreakHelper(s, wordDict, 0);
    }
    
    private boolean wordBreakHelper(String s, List<String> wordDict, int start) {
        if (start == s.length()) {
            return true;
        }
        
        for (String word : wordDict) {
            if (s.startsWith(word, start)) {
                if (wordBreakHelper(s, wordDict, start + word.length())) {
                    return true;
                }
            }
        }
        
        return false;
    }
}
```

# Memoized Approach
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Boolean[] memo = new Boolean[s.length()];
        return wordBreakHelper(s, wordDict, 0, memo);
    }
    
    private boolean wordBreakHelper(String s, List<String> wordDict, int start, Boolean[] memo) {
        if (start == s.length()) {
            return true;
        }
        
        if (memo[start] != null) {
            return memo[start];
        }
        
        for (String word : wordDict) {
            if (s.startsWith(word, start)) {
                if (wordBreakHelper(s, wordDict, start + word.length(), memo)) {
                    memo[start] = true;
                    return true;
                }
            }
        }
        
        memo[start] = false;
        return false;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] dp = new boolean[s.length() + 1];
        dp[s.length()] = true;
        
        for (int i = s.length() - 1; i >= 0; i--) {
            for (String word : wordDict) {
                if (i + word.length() <= s.length() && s.startsWith(word, i)) {
                    dp[i] = dp[i + word.length()];
                }
                if (dp[i]) {
                    break;
                }
            }
        }
        
        return dp[0];
    }
}
```