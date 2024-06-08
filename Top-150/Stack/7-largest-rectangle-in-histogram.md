[Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)

# Intuition
The problem is to find the area of the largest rectangle in a histogram represented by an array of bar heights. The intuition is to use a stack to keep track of the indices of the bars that are part of the potential largest rectangle. We can iterate through the heights and update the area whenever we encounter a bar that ends a potential largest rectangle.

# Approach
1. Create an empty stack `stack` to store the indices of the bars.
2. Initialize a variable `maxArea` to store the maximum area found so far.
3. Iterate through the `heights` array:
   a. While the stack is not empty, and the current height `heights[i]` is less than the height at the top of the stack `heights[stack.peek()]`, calculate the area of the potential largest rectangle with the height `heights[stack.peek()]` and the width determined by the indices in the stack. Update `maxArea` with the maximum of the current `maxArea` and the calculated area.
   b. Push the current index `i` onto the stack.
4. To handle the remaining bars in the stack, iterate while the stack is not empty:
   a. Calculate the area of the potential largest rectangle with the height `heights[stack.peek()]` and the width determined by the indices in the stack. Update `maxArea` with the maximum of the current `maxArea` and the calculated area.
   b. Pop the index from the stack.
5. Return `maxArea` as the area of the largest rectangle in the histogram.

# Complexity
- Time complexity: O(n)
* Space complexity: O(n)
The time complexity is O(n) because we iterate through the `heights` array once, and the operations on the stack take constant time on average. The space complexity is O(n) in the worst case, when all bars have the same height, and we need to store all indices in the stack.

# Code
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int maxArea = 0;
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i <= n; i++) {
            int currentHeight = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && currentHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }

            stack.push(i);
        }

        return maxArea;
    }
}
```