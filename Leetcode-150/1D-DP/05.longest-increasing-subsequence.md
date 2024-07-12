[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

# Intuition
The problem of finding the length of the longest increasing subsequence (LIS) can be solved using dynamic programming. The intuition behind the solution is to build the LIS by considering each element as a potential candidate for the LIS ending at that element. We can solve this problem by breaking it down into smaller subproblems and using the results of those subproblems to solve the larger problem.

# Approach
We can solve this problem using three different approaches:

1. Recursive Approach: We can recursively find the length of the LIS by considering each element as the potential end of the LIS. For each element, we recursively find the length of the LIS that ends at that element by considering all the elements after it. If an element is greater than the current element, we include it in the LIS and recursively find the length of the LIS ending at that element. We take the maximum length among all the possible LIS ending at each element.

2. Memoized Approach: To optimize the recursive approach, we can use memoization to store the previously calculated results and avoid redundant calculations. We use an array to store the length of the LIS ending at each index and retrieve them when needed.

3. Dynamic Programming Approach: We can use a bottom-up dynamic programming approach to solve this problem. We use an array `dp` where `dp[i]` represents the length of the LIS ending at index i. We iterate through the array and fill the `dp` array. For each index i, we find the maximum length of the LIS ending at i by considering all the elements before it. If an element before i is smaller than the current element, we include it in the LIS and update the length of the LIS ending at i.

# Complexity
- Time Complexity:
  - Recursive Approach: $$O(2^n)$$, where n is the length of the array. In the worst case, we have 2^n possible subsequences to consider.
  - Memoized Approach: $$O(n^2)$$, where n is the length of the array. We have n subproblems, and for each subproblem, we iterate through the elements after it, which can take up to n time.
  - Dynamic Programming Approach: $$O(n^2)$$, where n is the length of the array. We fill the `dp` array of size n, and for each index, we iterate through the elements before it, which can take up to n time.

- Space Complexity:
  - Recursive Approach: $$O(n)$$ to store the recursive call stack.
  - Memoized Approach: $$O(n)$$ to store the memoization array.
  - Dynamic Programming Approach: $$O(n)$$ to store the `dp` array.

# Recursive Approach
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int maxLength = 0;
        for (int i = 0; i < nums.length; i++) {
            maxLength = Math.max(maxLength, lengthOfLISHelper(nums, i));
        }
        
        return maxLength;
    }
    
    private int lengthOfLISHelper(int[] nums, int currentIndex) {
        int maxLength = 1;
        for (int i = currentIndex + 1; i < nums.length; i++) {
            if (nums[i] > nums[currentIndex]) {
                maxLength = Math.max(maxLength, 1 + lengthOfLISHelper(nums, i));
            }
        }
        
        return maxLength;
    }
}
```

# Memoized Approach
```java
class Solution {
    private int[] memo;
    
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int n = nums.length;
        memo = new int[n];
        Arrays.fill(memo, -1);
        
        int maxLength = 0;
        for (int i = 0; i < n; i++) {
            maxLength = Math.max(maxLength, lengthOfLISHelper(nums, i));
        }
        
        return maxLength;
    }
    
    private int lengthOfLISHelper(int[] nums, int currentIndex) {
        if (memo[currentIndex] != -1) {
            return memo[currentIndex];
        }
        
        int maxLength = 1;
        for (int i = currentIndex + 1; i < nums.length; i++) {
            if (nums[i] > nums[currentIndex]) {
                maxLength = Math.max(maxLength, 1 + lengthOfLISHelper(nums, i));
            }
        }
        
        memo[currentIndex] = maxLength;
        return maxLength;
    }
}
```

# Dynamic Programming Approach
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1);
        
        int maxLength = 1;
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], 1 + dp[j]);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }
        
        return maxLength;
    }
}
```