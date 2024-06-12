[House Robber](https://leetcode.com/problems/house-robber/)

# Intuition
The problem of house robber can be solved using dynamic programming. The intuition behind the solution is that at each house, we have two options: either rob the current house and add its amount to the maximum amount robbed from two houses before, or skip the current house and consider the maximum amount robbed from the previous house.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the maximum amount that can be robbed by considering the two options at each house: robbing the current house or skipping it.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the maximum amount that can be robbed for each house. We start from the base cases and build up the solution for the entire problem.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the number of houses. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(n)$$, where n is the number of houses. Memoization helps to avoid redundant calculations, reducing the time complexity to linear.
  - Dynamic Programming Approach: $$O(n)$$, where n is the number of houses. The dynamic programming approach iteratively calculates the maximum amount for each house, resulting in linear time complexity.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(n)$$ to store the DP array. However, it can be optimized to $$O(1)$$ by using variables instead of an array.

# Recursive Approach
```java
class Solution {
    public int rob(int[] nums) {
        return robHelper(nums, nums.length - 1);
    }
    
    private int robHelper(int[] nums, int index) {
        if (index < 0) {
            return 0;
        }
        return Math.max(nums[index] + robHelper(nums, index - 2), robHelper(nums, index - 1));
    }
}
```

# Memoized Approach
```java
class Solution {
    public int rob(int[] nums) {
        int[] memo = new int[nums.length];
        Arrays.fill(memo, -1);
        return robHelper(nums, nums.length - 1, memo);
    }
    
    private int robHelper(int[] nums, int index, int[] memo) {
        if (index < 0) {
            return 0;
        }
        if (memo[index] != -1) {
            return memo[index];
        }
        memo[index] = Math.max(nums[index] + robHelper(nums, index - 2, memo), robHelper(nums, index - 1, memo));
        return memo[index];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }
        
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        
        for (int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(nums[i] + dp[i - 2], dp[i - 1]);
        }
        
        return dp[nums.length - 1];
    }
}
```