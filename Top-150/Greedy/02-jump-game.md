[Jump Game](https://leetcode.com/problems/jump-game/description/)

# Intuition
The problem of determining if we can reach the end of the array by jumping can be solved using a recursive approach with memoization. The intuition is to start from the first index and recursively explore all possible jumps from each index. If we can reach the last index from any intermediate index, we can reach the end of the array. We can use memoization to avoid redundant recursive calls and optimize the solution.

# Approach
1. Create a memoization array `memo` of the same length as the input array and initialize it with `null` (representing an unvisited state).
2. Define a recursive function `jumpGame` that takes the current index, the input array `nums`, and the memoization array `memo` as parameters.
3. In the `jumpGame` function:
   - If the current index has already been visited (memoized), return the memoized result.
   - Base case: If the current index is the last index, return `true` since we have reached the end.
   - Iterate through all possible jumps from the current index (from 1 to `nums[index]`):
     - If the jump leads to a valid index within the array and recursively calling `jumpGame` from that index returns `true`, mark the current index as `true` in the memoization array and return `true`.
   - If no jump leads to the end, mark the current index as `false` in the memoization array and return `false`.
4. Call the `jumpGame` function with the starting index 0, the input array `nums`, and the memoization array `memo`, and return the result.

# Complexity
- Time complexity: O(n), where n is the length of the input array. Each index is visited at most once due to memoization, and the recursive calls explore a maximum of n-1 jumps.
- Space complexity: O(n) for the recursive call stack and the memoization array.

# Code
```java
class Solution {
    public boolean canJump(int[] nums) {
        // Create a memoization array and initialize with null (unvisited state)
        Boolean[] memo = new Boolean[nums.length];
        return jumpGame(0, nums, memo);
    }

    boolean jumpGame(int index, int[] nums, Boolean[] memo){
        // If we have already computed this subproblem, return the result
        if (memo[index] != null) {
            return memo[index];
        }

        // Base case: if we are at the last index
        if (index == nums.length - 1) {
            return true;
        }

        // Iterate through all jumps from the current index
        for (int i = 1; i <= nums[index]; i++) {
            if (index + i < nums.length && jumpGame(index + i, nums, memo)) {
                return memo[index] = true;
            }
        }

        // If no jump leads to the end, mark this index as false in memo
        return memo[index] = false;
    }
}
```