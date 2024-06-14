[Jump Game 2](https://leetcode.com/problems/jump-game-ii/description/)

# Intuition
The problem of finding the minimum number of jumps to reach the end of the array can be solved using a greedy approach. The intuition is to keep track of the farthest position we can reach from the current position and update it as we iterate through the array. We also need to keep track of the end of the current jump and increment the jump count whenever we reach the end of the current jump.

# Approach
1. If the length of the array is 1, return 0 since we are already at the end.
2. Initialize variables:
   - `jumps` to keep track of the minimum number of jumps, initially set to 0.
   - `currentEnd` to store the end of the current jump, initially set to 0.
   - `farthest` to store the farthest position we can reach from the current position, initially set to 0.
3. Iterate through the array from index 0 to the second-to-last index:
   - Update `farthest` by taking the maximum of `farthest` and `i + nums[i]`, where `i` is the current index. This represents the farthest position we can reach from the current position.
   - If the current index `i` is equal to `currentEnd`, it means we have reached the end of the current jump. In this case:
     - Increment `jumps` by 1 since we need to make a jump.
     - Update `currentEnd` to `farthest` to set the end of the next jump.
     - If `currentEnd` is greater than or equal to the last index of the array, it means we can reach the end from the current position, so we break out of the loop.
4. Return `jumps` as the minimum number of jumps required to reach the end of the array.

# Complexity
- Time complexity: O(n), where n is the length of the input array. We iterate through the array once.
- Space complexity: O(1) since we only use a constant amount of extra space for variables.

# Code
```java
class Solution {
    public int jump(int[] nums) {
        if (nums.length == 1) return 0;
        
        int jumps = 0;
        int currentEnd = 0;
        int farthest = 0;
        
        for (int i = 0; i < nums.length - 1; i++) {
            // Update the farthest we can reach from this position
            farthest = Math.max(farthest, i + nums[i]);
            
            // If we have reached the end of the current jump,
            // increase the jump count and update the end to the farthest we can reach
            if (i == currentEnd) {
                jumps++;
                currentEnd = farthest;
                
                // If we can reach the end from here, break
                if (currentEnd >= nums.length - 1) {
                    break;
                }
            }
        }
        
        return jumps;
    }
}
```