[Minimum Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

# Intuition
To solve the problem of finding the minimum cost to reach the top of the floor, we can use dynamic programming. The intuition is that at each step, we have two choices: either take one step or take two steps. We need to choose the option that minimizes the total cost.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the minimum cost to reach each step by taking the minimum of the cost of reaching the previous step plus the cost of the current step, and the cost of reaching two steps back plus the cost of the current step.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the minimum cost to reach each step. We start from the base cases and build up the solution for the entire array.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the number of steps. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(n)$$, where n is the number of steps. Memoization helps to avoid redundant calculations, reducing the time complexity to linear.
  - Dynamic Programming Approach: $$O(n)$$, where n is the number of steps. The dynamic programming approach iteratively calculates the minimum cost for each step, resulting in linear time complexity.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(1)$$ as we only need to store two variables to keep track of the minimum cost.

# Recursive Approach
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        return Math.min(minCostClimbingStairs(n - 1, cost), minCostClimbingStairs(n - 2, cost));
    }
    
    private int minCostClimbingStairs(int i, int[] cost) {
        if (i < 0) return 0;
        if (i == 0 || i == 1) return cost[i];
        
        return cost[i] + Math.min(minCostClimbingStairs(i - 1, cost), minCostClimbingStairs(i - 2, cost));
    }
}
```

# Memoized Approach
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int[] memo = new int[n];
        return Math.min(minCostClimbingStairs(n - 1, cost, memo), minCostClimbingStairs(n - 2, cost, memo));
    }
    
    private int minCostClimbingStairs(int i, int[] cost, int[] memo) {
        if (i < 0) return 0;
        if (i == 0 || i == 1) return cost[i];
        if (memo[i] != 0) return memo[i];
        
        memo[i] = cost[i] + Math.min(minCostClimbingStairs(i - 1, cost, memo), minCostClimbingStairs(i - 2, cost, memo));
        return memo[i];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        int prev1 = cost[0];
        int prev2 = cost[1];
        
        for (int i = 2; i < n; i++) {
            int curr = cost[i] + Math.min(prev1, prev2);
            prev1 = prev2;
            prev2 = curr;
        }
        
        return Math.min(prev1, prev2);
    }
}
```