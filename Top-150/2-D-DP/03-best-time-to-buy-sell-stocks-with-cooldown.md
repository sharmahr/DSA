[Best Time to Buy and Sell Stocks](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)

# Intuition
The problem of finding the maximum profit in stock trading with a cooldown can be solved using dynamic programming. The intuition behind the solution is to consider two states at each step: either the person is holding a stock or not holding a stock. We can make decisions based on these states and the current price, while also considering the cooldown constraint.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `dfs(prices, index, buying)` that takes the prices array, the current index, and a boolean indicating whether we are buying or selling.
   - Base case: If the index reaches the end of the prices array, return 0 since no more transactions can be made.
   - If we are in a buying state, we have two options:
     - Buy the stock at the current price and recursively call `dfs(prices, index + 1, !buying)` to move to the selling state.
     - Skip buying and recursively call `dfs(prices, index + 1, buying)` to move to the next day while staying in the buying state.
   - If we are in a selling state, we have two options:
     - Sell the stock at the current price and recursively call `dfs(prices, index + 2, !buying)` to move to the buying state after the cooldown day.
     - Skip selling and recursively call `dfs(prices, index + 1, buying)` to move to the next day while staying in the selling state.
   - Return the maximum profit obtained from the recursive calls.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization map to store the previously computed results.
   - Define a memoization map `cache` that uses a key combining the current index and the buying state.
   - Before making the recursive calls, check if the result for the current state is already computed and stored in the `cache`.
   - If the result is not computed, calculate it recursively and store it in the `cache` before returning.

3. Dynamic Programming Approach:
   - Define two arrays, `buy` and `sell`, of size `n+1` (where `n` is the length of the prices array) to store the maximum profit at each state.
   - Initialize `buy[0]` and `buy[1]` to `-prices[0]` (buying on the first day) and `-Math.min(prices[0], prices[1])` (buying on the second day or the first day, whichever is cheaper).
   - Initialize `sell[0]` and `sell[1]` to `0` (no stock to sell on the first day) and `Math.max(0, prices[1] - prices[0])` (selling on the second day if profitable).
   - Iterate through the prices array starting from index 2:
     - For the buying state, the maximum profit is either buying on the current day (`-prices[i] + sell[i-2]`) or carrying over the previous day's profit (`buy[i-1]`).
     - For the selling state, the maximum profit is either selling on the current day (`prices[i] + buy[i-1]`) or carrying over the previous day's profit (`sell[i-1]`).
   - Return the maximum profit at the end, which is `sell[n-1]`.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^n) in the worst case, where n is the length of the prices array. The recursive function explores all possible combinations of buying and selling.
  - Memoized Approach: O(n) as each state is computed only once and stored in the memoization map.
  - Dynamic Programming Approach: O(n) as we iterate through the prices array once to fill the DP arrays.

- Space Complexity:
  - Recursive Approach: O(n) for the recursive call stack.
  - Memoized Approach: O(n) to store the memoization map.
  - Dynamic Programming Approach: O(n) to store the DP arrays.

# Recursive Approach
```java
class Solution {
    public int maxProfit(int[] prices) {
        return dfs(prices, 0, true);
    }
    
    private int dfs(int[] prices, int index, boolean buying) {
        if (index >= prices.length) {
            return 0;
        }
        
        if (buying) {
            int buy = dfs(prices, index + 1, !buying) - prices[index];
            int skip = dfs(prices, index + 1, buying);
            return Math.max(buy, skip);
        } else {
            int sell = dfs(prices, index + 2, !buying) + prices[index];
            int skip = dfs(prices, index + 1, buying);
            return Math.max(sell, skip);
        }
    }
}
```

# Memoized Approach
```java
class Solution {
    public int maxProfit(int[] prices) {
        Map<String, Integer> cache = new HashMap<>();
        return dfs(prices, cache, 0, true);
    }
    
    private int dfs(int[] prices, Map<String, Integer> cache, int index, boolean buying) {
        if (index >= prices.length) {
            return 0;
        }
        
        String key = index + "-" + buying;
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        
        int cooldown = dfs(prices, cache, index + 1, buying);
        int buyOrSell = Integer.MIN_VALUE;
        
        if (buying) {
            buyOrSell = dfs(prices, cache, index + 1, !buying) - prices[index];
        } else {
            buyOrSell = dfs(prices, cache, index + 2, !buying) + prices[index];
        }
        
        cache.put(key, Math.max(buyOrSell, cooldown));
        return cache.get(key);
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        if (n <= 1) {
            return 0;
        }
        
        int[] buy = new int[n];
        int[] sell = new int[n];
        
        buy[0] = -prices[0];
        buy[1] = -Math.min(prices[0], prices[1]);
        sell[0] = 0;
        sell[1] = Math.max(0, prices[1] - prices[0]);
        
        for (int i = 2; i < n; i++) {
            buy[i] = Math.max(-prices[i] + sell[i-2], buy[i-1]);
            sell[i] = Math.max(prices[i] + buy[i-1], sell[i-1]);
        }
        
        return sell[n-1];
    }
}
```