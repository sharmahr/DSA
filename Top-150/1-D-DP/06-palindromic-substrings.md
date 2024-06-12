[Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/description/)

# Intuition
To count the number of palindromic substrings, we can consider each character in the string as the center of a potential palindrome and expand outwards from that center. We need to consider both odd-length and even-length palindromes.

# Approach
We can solve this problem using three different approaches:

1. Brute Force Approach: Generate all possible substrings and check if each substring is a palindrome. Increment the count for each palindromic substring found.

2. Dynamic Programming Approach: Use a 2D boolean array to store whether a substring is a palindrome or not. Fill the array in a bottom-up manner by considering substrings of different lengths. Increment the count for each palindromic substring found.

3. Expand Around Center Approach: Iterate through each character of the string and consider it as the center of a potential palindrome. Expand outwards from the center character to find palindromic substrings centered at that position. Consider both odd-length and even-length palindromes. Increment the count for each palindromic substring found.

# Complexity
- Time Complexity:
  - Brute Force Approach: $$O(n^3)$$, where n is the length of the string. Generating all substrings takes $$O(n^2)$$ time, and checking each substring for palindrome property takes $$O(n)$$ time.
  - Dynamic Programming Approach: $$O(n^2)$$, where n is the length of the string. Filling the 2D array requires nested loops, resulting in quadratic time complexity.
  - Expand Around Center Approach: $$O(n^2)$$, where n is the length of the string. We iterate through each character and expand outwards, resulting in quadratic time complexity in the worst case.

- Space Complexity:
  - Brute Force Approach: $$O(1)$$ as we only need to store the count of palindromic substrings.
  - Dynamic Programming Approach: $$O(n^2)$$ to store the 2D boolean array.
  - Expand Around Center Approach: $$O(1)$$ as we only need to store the count of palindromic substrings.

# Recursive Approach
```java
class Solution {
    public int countSubstrings(String s) {
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            count += countPalindromesAroundCenter(s, i, i);      // Odd-length palindromes
            count += countPalindromesAroundCenter(s, i, i + 1);  // Even-length palindromes
        }
        return count;
    }
    
    private int countPalindromesAroundCenter(String s, int left, int right) {
        int count = 0;
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            count++;
            left--;
            right++;
        }
        return count;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int countSubstrings(String s) {
        int n = s.length();
        int[][] memo = new int[n][n];
        int count = 0;
        for (int i = 0; i < n; i++) {
            count += countPalindromesAroundCenter(s, i, i, memo);      // Odd-length palindromes
            count += countPalindromesAroundCenter(s, i, i + 1, memo);  // Even-length palindromes
        }
        return count;
    }
    
    private int countPalindromesAroundCenter(String s, int left, int right, int[][] memo) {
        if (left < 0 || right >= s.length() || s.charAt(left) != s.charAt(right)) {
            return 0;
        }
        if (memo[left][right] != 0) {
            return memo[left][right];
        }
        int count = 1 + countPalindromesAroundCenter(s, left - 1, right + 1, memo);
        memo[left][right] = count;
        return count;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int countSubstrings(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int count = 0;
        
        // All substrings of length 1 are palindromes
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            count++;
        }
        
        // Check substrings of length 2
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                count++;
            }
        }
        
        // Check substrings of length greater than 2
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    count++;
                }
            }
        }
        
        return count;
    }
}
```