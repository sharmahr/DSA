[Target Sum](https://leetcode.com/problems/target-sum/description/)

# Intuition
The problem of finding the number of ways to assign symbols to make the sum of integers equal to the target sum can be solved using dynamic programming. The intuition behind the solution is to consider the problem as a subset sum problem. We can partition the array into two subsets, one with positive integers and the other with negative integers, such that the sum of the positive subset minus the sum of the negative subset equals the target sum.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach:
   - Define a recursive function `findTargetSumWays(nums, target, index, currentSum)` that takes the array of integers, the target sum, the current index, and the current sum as parameters.
   - Base cases:
     - If the index reaches the end of the array and the current sum equals the target sum, return 1 since we have found a valid assignment.
     - If the index reaches the end of the array and the current sum does not equal the target sum, return 0 since it is an invalid assignment.
   - Recursive calls:
     - Assign a positive sign to the current integer: Recursively call `findTargetSumWays(nums, target, index + 1, currentSum + nums[index])`.
     - Assign a negative sign to the current integer: Recursively call `findTargetSumWays(nums, target, index + 1, currentSum - nums[index])`.
   - Return the sum of the results from the recursive calls.

2. Memoized Approach:
   - Similar to the recursive approach, but use a memoization table to store the previously computed results.
   - Define a 2D memoization table `memo` of size `(number of integers) × (target sum + 1)` initialized with -1 to indicate uncomputed states.
   - Modify the recursive function to first check if the result for the current state is already computed and stored in `memo`.
   - If the result is not computed, calculate it recursively and store it in `memo` before returning.

3. Dynamic Programming Approach:
   - Observe that the problem can be converted to a subset sum problem.
   - Calculate the total sum of all integers in the array.
   - If the total sum is less than the absolute value of the target sum or if the total sum and target sum have different parities, return 0 since no valid assignment exists.
   - Create a 1D DP table `dp` of size `(total sum + 1)` initialized with 0.
   - Initialize `dp[0] = 1` since there is one way to achieve a sum of 0 (by not selecting any integers).
   - Iterate through each integer in the array.
   - For each integer, update the `dp` table by iterating from the total sum down to the current integer.
   - Update `dp[i]` by adding the number of ways to achieve the sum `i` without including the current integer (`dp[i]`) and the number of ways to achieve the sum `i - num` by including the current integer (`dp[i - num]`).
   - Return `dp[target]` as the final result.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^n) in the worst case, where n is the number of integers in the array. The recursive function explores all possible combinations of assigning positive and negative signs to each integer.
  - Memoized Approach: O(n * target) as each subproblem is solved only once and stored in the memoization table.
  - Dynamic Programming Approach: O(n * target) as we iterate through each integer and update the `dp` table.

- Space Complexity:
  - Recursive Approach: O(n) for the recursive call stack.
  - Memoized Approach: O(n * target) to store the memoization table.
  - Dynamic Programming Approach: O(target) to store the `dp` table.

# Recursive Approach
```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        return findTargetSumWaysHelper(nums, target, 0, 0);
    }
    
    private int findTargetSumWaysHelper(int[] nums, int target, int index, int currentSum) {
        if (index == nums.length) {
            if (currentSum == target) {
                return 1;
            }
            return 0;
        }
        
        int positive = findTargetSumWaysHelper(nums, target, index + 1, currentSum + nums[index]);
        int negative = findTargetSumWaysHelper(nums, target, index + 1, currentSum - nums[index]);
        
        return positive + negative;
    }
}
```

# Memoized Approach
```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int[][] memo = new int[nums.length + 1][2001];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        return findTargetSumWaysHelper(nums, target, 0, 0, memo);
    }
    
    private int findTargetSumWaysHelper(int[] nums, int target, int index, int currentSum, int[][] memo) {
        if (index == nums.length) {
            if (currentSum == target) {
                return 1;
            }
            return 0;
        }
        
        if (memo[index][currentSum + 1000] != -1) {
            return memo[index][currentSum + 1000];
        }
        
        int positive = findTargetSumWaysHelper(nums, target, index + 1, currentSum + nums[index], memo);
        int negative = findTargetSumWaysHelper(nums, target, index + 1, currentSum - nums[index], memo);
        
        memo[index][currentSum + 1000] = positive + negative;
        return memo[index][currentSum + 1000];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }
        
        if (totalSum < Math.abs(target) || (totalSum + target) % 2 != 0) {
            return 0;
        }
        
        int sum = (totalSum + target) / 2;
        int[] dp = new int[sum + 1];
        dp[0] = 1;
        
        for (int num : nums) {
            for (int i = sum; i >= num; i--) {
                dp[i] += dp[i - num];
            }
        }
        
        return dp[sum];
    }
}
```