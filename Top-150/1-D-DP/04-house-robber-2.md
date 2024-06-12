[House Robber 2](https://leetcode.com/problems/house-robber-ii/) 

# Intuition
The problem of robbing houses in a circular arrangement can be solved by considering two cases: either the first house is robbed or the last house is robbed. We can calculate the maximum amount that can be robbed for each case and take the maximum of the two.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively calculate the maximum amount that can be robbed by considering the two cases: robbing the houses from index 0 to n-2 (excluding the last house) or robbing the houses from index 1 to n-1 (excluding the first house).

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to iteratively calculate the maximum amount that can be robbed for each subproblem. We can solve the problem for the two cases separately and take the maximum of the two.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the number of houses. The recursive approach has exponential time complexity due to the redundant calculations.
  - Memoized Approach: $$O(n)$$, where n is the number of houses. Memoization helps to avoid redundant calculations, reducing the time complexity to linear.
  - Dynamic Programming Approach: $$O(n)$$, where n is the number of houses. The dynamic programming approach iteratively calculates the maximum amount for each subproblem, resulting in linear time complexity.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(1)$$ as we only need to store a constant number of variables.

# Recursive Approach
```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }
        return Math.max(robHelper(nums, 0, nums.length - 2), robHelper(nums, 1, nums.length - 1));
    }
    
    private int robHelper(int[] nums, int start, int end) {
        if (start > end) {
            return 0;
        }
        return Math.max(nums[start] + robHelper(nums, start + 2, end), robHelper(nums, start + 1, end));
    }
}
```

# Memoized Approach
```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return nums[0];
        }
        int[][] memo = new int[nums.length][2];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return Math.max(robHelper(nums, 0, nums.length - 2, memo), robHelper(nums, 1, nums.length - 1, memo));
    }
    
    private int robHelper(int[] nums, int start, int end, int[][] memo) {
        if (start > end) {
            return 0;
        }
        if (memo[start][end - start] != -1) {
            return memo[start][end - start];
        }
        memo[start][end - start] = Math.max(nums[start] + robHelper(nums, start + 2, end, memo), robHelper(nums, start + 1, end, memo));
        return memo[start][end - start];
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
        return Math.max(robHelper(nums, 0, nums.length - 2), robHelper(nums, 1, nums.length - 1));
    }
    
    private int robHelper(int[] nums, int start, int end) {
        int rob1 = 0;
        int rob2 = 0;
        
        for (int i = start; i <= end; i++) {
            int temp = Math.max(rob1 + nums[i], rob2);
            rob1 = rob2;
            rob2 = temp;
        }
        
        return rob2;
    }
}
```