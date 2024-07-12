[Rotate Image](https://leetcode.com/problems/rotate-image/description/)

# Intuition
The problem is to rotate a square matrix by 90 degrees clockwise in-place. The intuition is to perform the rotation in layers, starting from the outermost layer and moving inwards. In each layer, we swap the elements of the top, right, bottom, and left sides of the layer in a cyclic manner.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the start and end indices of the current layer, respectively.
2. While `left` is less than `right`, perform the following steps for each layer:
   - Initialize a variable `top` to `left` and `bottom` to `right`.
   - Iterate `i` from 0 to `right - left` (exclusive) to traverse the elements in the current layer.
   - Save the top-left element of the current layer in a variable `topLeft`.
   - Move the bottom-left element to the top-left position.
   - Move the bottom-right element to the bottom-left position.
   - Move the top-right element to the bottom-right position.
   - Move the saved `topLeft` element to the top-right position.
   - Increment `left` and decrement `right` to move to the next inner layer.
3. Repeat step 2 until all layers are processed.

# Complexity
- Time complexity: $O(n^2)$, where $n$ is the number of rows/columns in the matrix.
  - We process each element in the matrix once, and the total number of elements is $n^2$.
- Space complexity: $O(1)$
  - We perform the rotation in-place without using any extra space.

# Code
```java
class Solution {
    public void rotate(int[][] matrix) {
        int left = 0;
        int right = matrix.length - 1;
        while (left < right) {
            for (int i = 0; i < right - left; i++) {
                int top = left;
                int bottom = right;

                // Save the top-left element
                int topLeft = matrix[top][left + i];

                // Move bottom-left to top-left
                matrix[top][left + i] = matrix[bottom - i][left];

                // Move bottom-right to bottom-left
                matrix[bottom - i][left] = matrix[bottom][right - i];

                // Move top-right to bottom-right
                matrix[bottom][right - i] = matrix[top + i][right];

                // Move top-left to top-right
                matrix[top + i][right] = topLeft;
            }

            right -= 1;
            left += 1;
        }
    }
}
```