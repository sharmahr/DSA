[Container with Most Water](https://leetcode.com/problems/container-with-most-water/description/)

# Intuition
The problem asks to find the maximum area of a container formed by two vertical lines in a histogram represented by an array of heights. The intuition is to use two pointers, one at the beginning and one at the end of the array, and move them inwards to find the maximum area. The area is determined by the smaller of the two heights and the distance between the two lines.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the first and last indices of the array, respectively.
2. Initialize a variable `maxArea` to keep track of the maximum area found so far.
3. While `left` is less than `right`, do the following:
   a. Calculate the width as `right - left`.
   b. Calculate the height as the minimum of `height[left]` and `height[right]`.
   c. Calculate the current area as `width * height`.
   d. Update `maxArea` with the maximum of `maxArea` and the current area.
   e. Move the pointer pointing to the shorter line inwards (towards the other pointer) to potentially find a larger area.
4. Return `maxArea` as the maximum area of the container.

# Complexity
- Time complexity: O(n), where n is the length of the input array. In the worst case, we need to iterate through the entire array once.
- Space complexity: O(1), as we are using only a constant amount of extra space for pointers and temporary variables.

# Code
```java
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0;
        int right = height.length - 1;

        while (left < right) {
            int width = right - left;
            int currentArea = Math.min(height[left], height[right]) * width;
            maxArea = Math.max(maxArea, currentArea);

            // Move the pointer that points to the shorter line
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;
    }
}
```