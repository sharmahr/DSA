[Rainwater Trapping](https://leetcode.com/problems/trapping-rain-water/description/)

# Intuition
The problem asks to find the amount of water that can be trapped after raining in a given elevation map represented by an array of heights. The intuition is to use two pointers, one starting from the left and the other from the right, and keep track of the maximum height seen from both sides. The amount of water trapped at any point is determined by the minimum of the maximum heights on both sides and the current height.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the first and last indices of the array, respectively.
2. Initialize two variables, `leftMax` and `rightMax`, to keep track of the maximum heights seen from the left and right sides, respectively.
3. Initialize a variable `waterTrapped` to accumulate the amount of water trapped.
4. While `left` is less than `right`, do the following:
   a. If the height at `left` is smaller than the height at `right`:
      - If the height at `left` is greater than or equal to `leftMax`, update `leftMax` to the height at `left`.
      - Otherwise, add the difference between `leftMax` and the height at `left` to `waterTrapped`.
   b. If the height at `right` is smaller than or equal to the height at `left`:
      - If the height at `right` is greater than or equal to `rightMax`, update `rightMax` to the height at `right`.
      - Otherwise, add the difference between `rightMax` and the height at `right` to `waterTrapped`.
   c. Move `left` forward if the height at `left` is smaller than the height at `right`, or move `right` backward if the height at `right` is smaller than or equal to the height at `left`.
5. Return `waterTrapped` as the total amount of water trapped.

# Complexity
- Time complexity: O(n), where n is the length of the input array. In the worst case, we need to iterate through the entire array once.
- Space complexity: O(1), as we are using only a constant amount of extra space for pointers and temporary variables.

# Code
```java
class Solution {
    public int trap(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }

        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int waterTrapped = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    waterTrapped += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    waterTrapped += rightMax - height[right];
                }
                right--;
            }
        }

        return waterTrapped;
    }
}
```