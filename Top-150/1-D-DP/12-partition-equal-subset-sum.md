[Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

# Intuition
The problem of determining if a given set of positive integers can be partitioned into two subsets with equal sums can be solved using dynamic programming. The intuition behind the solution is to find a subset of the given set whose sum is equal to half of the total sum of all the integers. If such a subset exists, then the remaining elements will form the other subset with an equal sum, resulting in a valid partition.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively generate all possible subsets and check if any subset has a sum equal to half of the total sum. If we find such a subset, we can conclude that the set can be partitioned into two equal-sum subsets.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use a 2D boolean array to store the results of subproblems, where each entry represents whether a subset with a specific sum can be formed using a certain number of elements.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to solve this problem efficiently. We use a 1D boolean array `dp` where `dp[i]` represents whether a subset with a sum equal to `i` can be formed. We iterate through each element and update the `dp` array accordingly. If `dp[target]` is true at the end, where `target` is half of the total sum, then the set can be partitioned into two equal-sum subsets.

# Complexity
- Time Complexity:
  - Recursive Approach: O(2^n), where n is the number of elements in the set. In the worst case, we generate all possible subsets, which is exponential.
  - Memoized Approach: O(n * sum), where n is the number of elements in the set and sum is the total sum of all elements. We have n * sum subproblems, and each subproblem takes constant time to solve.
  - Dynamic Programming Approach: O(n * sum), where n is the number of elements in the set and sum is the total sum of all elements. We fill the `dp` array of size sum/2, and for each element, we update the `dp` array, which takes O(sum) time.

- Space Complexity:
  - Recursive Approach: O(n) to store the recursive call stack.
  - Memoized Approach: O(n * sum) to store the memoization array.
  - Dynamic Programming Approach: O(sum) to store the `dp` array.

# Recursive Approach
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        
        if (sum % 2 != 0) {
            return false;
        }
        
        return canPartitionHelper(nums, 0, sum / 2);
    }
    
    private boolean canPartitionHelper(int[] nums, int index, int target) {
        if (target == 0) {
            return true;
        }
        
        if (index == nums.length || target < 0) {
            return false;
        }
        
        // Include the current element in the subset
        if (canPartitionHelper(nums, index + 1, target - nums[index])) {
            return true;
        }
        
        // Exclude the current element from the subset
        return canPartitionHelper(nums, index + 1, target);
    }
}
```

# Memoized Approach
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        
        if (sum % 2 != 0) {
            return false;
        }
        
        int target = sum / 2;
        Boolean[][] memo = new Boolean[nums.length][target + 1];
        return canPartitionHelper(nums, 0, target, memo);
    }
    
    private boolean canPartitionHelper(int[] nums, int index, int target, Boolean[][] memo) {
        if (target == 0) {
            return true;
        }
        
        if (index == nums.length || target < 0) {
            return false;
        }
        
        if (memo[index][target] != null) {
            return memo[index][target];
        }
        
        // Include the current element in the subset
        if (canPartitionHelper(nums, index + 1, target - nums[index], memo)) {
            memo[index][target] = true;
            return true;
        }
        
        // Exclude the current element from the subset
        memo[index][target] = canPartitionHelper(nums, index + 1, target, memo);
        return memo[index][target];
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        
        if (sum % 2 != 0) {
            return false;
        }
        
        int target = sum / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true; // Base case: zero sum is always possible with empty subset
        
        for (int num : nums) {
            for (int i = target; i >= num; i--) {
                dp[i] = dp[i] || dp[i - num];
            }
        }
        
        return dp[target];
    }
}
```