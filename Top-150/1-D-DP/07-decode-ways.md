[Decode Ways](https://leetcode.com/problems/decode-ways/description/)

# Intuition
The problem of decoding a string can be solved using dynamic programming. The intuition behind the solution is that at each position in the string, we have two options: either decode a single digit or decode two digits (if possible). We need to consider all possible combinations of decoding and count the total number of ways.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the number of ways to decode the string by considering the two options at each position: decoding a single digit or decoding two digits (if possible). We recursively solve the subproblems and combine their results.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use an array to store the intermediate results and retrieve them when needed.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the number of ways to decode the string. We start from the base cases and build up the solution for the entire string.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the length of the string. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(n)$$, where n is the length of the string. Memoization helps to avoid redundant calculations, reducing the time complexity to linear.
  - Dynamic Programming Approach: $$O(n)$$, where n is the length of the string. The dynamic programming approach iteratively calculates the number of ways for each position, resulting in linear time complexity.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(n)$$ to store the DP array. However, it can be optimized to $$O(1)$$ by using variables instead of an array.

# Recursive Approach
```java
class Solution {
    public int numDecodings(String s) {
        return numDecodingsHelper(s, 0);
    }
    
    private int numDecodingsHelper(String s, int index) {
        if (index == s.length()) {
            return 1;
        }
        if (s.charAt(index) == '0') {
            return 0;
        }
        
        int count = numDecodingsHelper(s, index + 1);
        if (index < s.length() - 1 && (s.charAt(index) == '1' || (s.charAt(index) == '2' && s.charAt(index + 1) <= '6'))) {
            count += numDecodingsHelper(s, index + 2);
        }
        
        return count;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int numDecodings(String s) {
        int[] memo = new int[s.length()];
        Arrays.fill(memo, -1);
        return numDecodingsHelper(s, 0, memo);
    }
    
    private int numDecodingsHelper(String s, int index, int[] memo) {
        if (index == s.length()) {
            return 1;
        }
        if (s.charAt(index) == '0') {
            return 0;
        }
        if (memo[index] != -1) {
            return memo[index];
        }
        
        int count = numDecodingsHelper(s, index + 1, memo);
        if (index < s.length() - 1 && (s.charAt(index) == '1' || (s.charAt(index) == '2' && s.charAt(index + 1) <= '6'))) {
            count += numDecodingsHelper(s, index + 2, memo);
        }
        
        memo[index] = count;
        return count;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int numDecodings(String s) {
        int n = s.length();
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = (s.charAt(0) == '0') ? 0 : 1;
        
        for (int i = 2; i <= n; i++) {
            if (s.charAt(i - 1) != '0') {
                dp[i] += dp[i - 1];
            }
            if (s.charAt(i - 2) == '1' || (s.charAt(i - 2) == '2' && s.charAt(i - 1) <= '6')) {
                dp[i] += dp[i - 2];
            }
        }
        
        return dp[n];
    }
}
```