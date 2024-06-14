[Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

# Intuition
The problem of finding the contiguous subarray with the largest sum can be solved using Kadane's algorithm. The intuition behind Kadane's algorithm is to maintain a variable that stores the maximum sum ending at the current position and another variable that keeps track of the overall maximum sum encountered so far. At each step, we decide whether to start a new subarray or continue the existing subarray based on whether including the current element increases the sum or not.

# Approach
1. Initialize two variables:
   - `maxSum` to store the overall maximum sum, initialized to the first element of the array.
   - `currentSum` to store the maximum sum ending at the current position, initialized to the first element of the array.
2. Iterate through the array starting from the second element:
   - Update `currentSum` by taking the maximum of either including the current element (`nums[i] + currentSum`) or starting a new subarray from the current element (`nums[i]`).
   - Update `maxSum` by taking the maximum of `currentSum` and `maxSum`.
3. Return `maxSum` as the result.

# Complexity
- Time complexity: O(n), where n is the length of the input array. The algorithm iterates through the array once.
- Space complexity: O(1) since only a constant amount of extra space is used for variables.

# Code
```java
class Solution {
    public int maxSubArray(int[] nums) {
        // kadanes algorithm
        int maxSum = nums[0];
        int currentSum = nums[0];

        for(int i=1;i<nums.length;i++){
            // update the current sum by either including the current element or starting a new subarray
            currentSum = Math.max(nums[i], nums[i] + currentSum);
            maxSum = Math.max(currentSum, maxSum);
        }

        return maxSum;
    }
}
```