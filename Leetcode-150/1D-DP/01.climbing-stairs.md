[Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

# Intuition
The problem of climbing stairs can be solved using dynamic programming. The intuition behind the solution is that to reach the nth step, we can either climb 1 step from the (n-1)th step or 2 steps from the (n-2)th step. This forms a recursive pattern similar to the Fibonacci sequence.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the number of ways to reach the nth step by summing up the number of ways to reach the (n-1)th step and the (n-2)th step.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the number of ways to reach each step. We start from the base cases and build up the solution for the entire problem.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the number of steps. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(n)$$, where n is the number of steps. Memoization helps to avoid redundant calculations, reducing the time complexity to linear.
  - Dynamic Programming Approach: $$O(n)$$, where n is the number of steps. The dynamic programming approach iteratively calculates the number of ways for each step, resulting in linear time complexity.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(n)$$ to store the DP array. However, it can be optimized to $$O(1)$$ by using variables instead of an array.

# Recursive Approach
```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }
        return climbStairs(n - 1) + climbStairs(n - 2);
    }
}
```

# Memoized Approach
```java
class Solution {
    public int climbStairs(int n) {
        int[] memo = new int[n + 1];
        return climbStairsMemo(n, memo);
    }
    
    private int climbStairsMemo(int n, int[] memo) {
        if (n <= 2) {
            return n;
        }
        if (memo[n] != 0) {
            return memo[n];
        }
        memo[n] = climbStairsMemo(n - 1, memo) + climbStairsMemo(n - 2, memo);
        return memo[n];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
}
```
