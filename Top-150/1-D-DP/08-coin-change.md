[Coin Change](https://leetcode.com/problems/coin-change/description/)

# Intuition
The problem of finding the minimum number of coins to make up a given amount can be solved using dynamic programming. The intuition behind the solution is that for each amount, we can choose any coin denomination and recursively solve the subproblem for the remaining amount. We need to consider all possible coin denominations and find the minimum number of coins needed.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the minimum number of coins needed to make up the given amount by considering all possible coin denominations at each step. We choose each coin denomination and recursively solve the subproblem for the remaining amount. The base case is when the amount becomes zero.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use an array to store the intermediate results and retrieve them when needed.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the minimum number of coins needed for each amount from 0 to the target amount. We start from the base case of 0 amount and build up the solution for the target amount.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(S^n)$$, where S is the target amount and n is the number of coin denominations. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(S * n)$$, where S is the target amount and n is the number of coin denominations. Memoization helps to avoid redundant calculations, reducing the time complexity to polynomial.
  - Dynamic Programming Approach: $$O(S * n)$$, where S is the target amount and n is the number of coin denominations. The dynamic programming approach iteratively calculates the minimum number of coins for each amount, resulting in polynomial time complexity.

- Space Complexity:
  - Recursive Approach: $$O(S)$$ to store the recursive call stack.
  - Memoized Approach: $$O(S)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(S)$$ to store the DP array.

# Recursive Approach
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        return coinChangeHelper(coins, amount);
    }
    
    private int coinChangeHelper(int[] coins, int amount) {
        if (amount == 0) {
            return 0;
        }
        if (amount < 0) {
            return -1;
        }
        
        int minCoins = Integer.MAX_VALUE;
        for (int coin : coins) {
            int subResult = coinChangeHelper(coins, amount - coin);
            if (subResult != -1) {
                minCoins = Math.min(minCoins, 1 + subResult);
            }
        }
        
        return minCoins != Integer.MAX_VALUE ? minCoins : -1;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] memo = new int[amount + 1];
        Arrays.fill(memo, -2);
        return coinChangeHelper(coins, amount, memo);
    }
    
    private int coinChangeHelper(int[] coins, int amount, int[] memo) {
        if (amount == 0) {
            return 0;
        }
        if (amount < 0) {
            return -1;
        }
        if (memo[amount] != -2) {
            return memo[amount];
        }
        
        int minCoins = Integer.MAX_VALUE;
        for (int coin : coins) {
            int subResult = coinChangeHelper(coins, amount - coin, memo);
            if (subResult != -1) {
                minCoins = Math.min(minCoins, 1 + subResult);
            }
        }
        
        memo[amount] = minCoins != Integer.MAX_VALUE ? minCoins : -1;
        return memo[amount];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        
        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```