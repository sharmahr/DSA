[Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

# Intuition
To find the longest palindromic substring, we can consider each character in the string as the center of a potential palindrome and expand outwards from that center. We need to consider both odd-length and even-length palindromes.

# Approach
We can solve this problem using three different approaches:

1. Brute Force Approach: Generate all possible substrings and check if each substring is a palindrome. Update the result with the longest palindromic substring found.

2. Dynamic Programming Approach: Use a 2D boolean array to store whether a substring is a palindrome or not. Fill the array in a bottom-up manner by considering substrings of different lengths.

3. Expand Around Center Approach: Iterate through each character of the string and consider it as the center of a potential palindrome. Expand outwards from the center character to find the longest palindrome centered at that position. Consider both odd-length and even-length palindromes.

# Complexity
- Time Complexity:
  - Brute Force Approach: $$O(n^3)$$, where n is the length of the string. Generating all substrings takes $$O(n^2)$$ time, and checking each substring for palindrome property takes $$O(n)$$ time.
  - Dynamic Programming Approach: $$O(n^2)$$, where n is the length of the string. Filling the 2D array requires nested loops, resulting in quadratic time complexity.
  - Expand Around Center Approach: $$O(n^2)$$, where n is the length of the string. We iterate through each character and expand outwards, resulting in quadratic time complexity in the worst case.

- Space Complexity:
  - Brute Force Approach: $$O(1)$$ as we only need to store the longest palindromic substring found so far.
  - Dynamic Programming Approach: $$O(n^2)$$ to store the 2D boolean array.
  - Expand Around Center Approach: $$O(1)$$ as we only need to store the longest palindromic substring found so far.

# Recursive Approach
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }
        return longestPalindromeHelper(s, 0, s.length() - 1);
    }
    
    private String longestPalindromeHelper(String s, int left, int right) {
        if (left > right) {
            return "";
        }
        if (left == right) {
            return s.substring(left, left + 1);
        }
        if (s.charAt(left) == s.charAt(right) && longestPalindromeHelper(s, left + 1, right - 1).length() == right - left - 1) {
            return s.substring(left, right + 1);
        }
        String leftPalindrome = longestPalindromeHelper(s, left + 1, right);
        String rightPalindrome = longestPalindromeHelper(s, left, right - 1);
        return leftPalindrome.length() > rightPalindrome.length() ? leftPalindrome : rightPalindrome;
    }
}
```

# Memoized Approach
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }
        String[][] memo = new String[s.length()][s.length()];
        return longestPalindromeHelper(s, 0, s.length() - 1, memo);
    }
    
    private String longestPalindromeHelper(String s, int left, int right, String[][] memo) {
        if (left > right) {
            return "";
        }
        if (left == right) {
            return s.substring(left, left + 1);
        }
        if (memo[left][right] != null) {
            return memo[left][right];
        }
        if (s.charAt(left) == s.charAt(right) && longestPalindromeHelper(s, left + 1, right - 1, memo).length() == right - left - 1) {
            memo[left][right] = s.substring(left, right + 1);
            return memo[left][right];
        }
        String leftPalindrome = longestPalindromeHelper(s, left + 1, right, memo);
        String rightPalindrome = longestPalindromeHelper(s, left, right - 1, memo);
        memo[left][right] = leftPalindrome.length() > rightPalindrome.length() ? leftPalindrome : rightPalindrome;
        return memo[left][right];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 2) {
            return s;
        }
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        String longest = "";
        
        // All substrings of length 1 are palindromes
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            longest = s.substring(i, i + 1);
        }
        
        // Check substrings of length 2
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                longest = s.substring(i, i + 2);
            }
        }
        
        // Check substrings of length greater than 2
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    longest = s.substring(i, j + 1);
                }
            }
        }
        
        return longest;
    }
}
```