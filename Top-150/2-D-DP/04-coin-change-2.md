[Coin Change](https://leetcode.com/problems/coin-change-ii/description/)

# Intuition
The problem of counting the number of coin combinations that make up a given amount can be solved using dynamic programming. The intuition behind the solution is to consider each coin denomination and determine the number of ways to make up the remaining amount using the available coins. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `countCombinations(amount, coins, index)` that takes the remaining amount, the array of coin denominations, and the current index as parameters.
   - Base cases:
     - If the remaining amount is 0, return 1 since we have found a valid combination.
     - If the remaining amount is less than 0 or the index exceeds the number of coins, return 0 since it is an invalid combination.
   - Recursive calls:
     - Include the current coin: Recursively call `countCombinations(amount - coins[index], coins, index)` to consider including the current coin.
     - Exclude the current coin: Recursively call `countCombinations(amount, coins, index + 1)` to move to the next coin without including the current coin.
   - Return the sum of the results from the recursive calls.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(number of coins) × (amount + 1)` initialized with -1 to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Create a 1D DP table `dp` of size `amount + 1` initialized with 0.
   - Initialize the base case: `dp[0] = 1` since there is one way to make up an amount of 0 (by not selecting any coins).
   - Iterate through each coin denomination.
   - For each coin, iterate through the amounts from the coin value to the target amount.
   - Update `dp[i]` by adding the number of combinations obtained by excluding the current coin (`dp[i]`) and including the current coin (`dp[i - coin]`).
   - Return `dp[amount]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^(n * amount)) in the worst case, where n is the number of coins and amount is the target amount. The recursive function explores all possible combinations of including or excluding each coin.
  - Memoized Approach: O(n * amount) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(n * amount) as we iterate through each coin and amount combination.

- Space Complexity:
  - Recursive Approach: O(n * amount) for the recursive call stack.
  - Memoized Approach: O(n * amount) to store the memoization table.
  - Dynamic Programming Approach: O(amount) to store the DP table.

# Recursive Approach
```java
class Solution {
    public int change(int amount, int[] coins) {
        return countCombinations(amount, coins, 0);
    }
    
    private int countCombinations(int amount, int[] coins, int index) {
        if (amount == 0) {
            return 1;
        }
        if (amount < 0 || index >= coins.length) {
            return 0;
        }
        
        int includeCurrentCoin = countCombinations(amount - coins[index], coins, index);
        int excludeCurrentCoin = countCombinations(amount, coins, index + 1);
        
        return includeCurrentCoin + excludeCurrentCoin;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int change(int amount, int[] coins) {
        int[][] memo = new int[coins.length][amount + 1];
        for (int i = 0; i < coins.length; i++) {
            for (int j = 0; j <= amount; j++) {
                memo[i][j] = -1;
            }
        }
        return countCombinations(amount, coins, 0, memo);
    }
    
    private int countCombinations(int amount, int[] coins, int index, int[][] memo) {
        if (amount == 0) {
            return 1;
        }
        if (amount < 0 || index >= coins.length) {
            return 0;
        }
        
        if (memo[index][amount] != -1) {
            return memo[index][amount];
        }
        
        int includeCurrentCoin = countCombinations(amount - coins[index], coins, index, memo);
        int excludeCurrentCoin = countCombinations(amount, coins, index + 1, memo);
        
        memo[index][amount] = includeCurrentCoin + excludeCurrentCoin;
        return memo[index][amount];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        
        return dp[amount];
    }
}
```