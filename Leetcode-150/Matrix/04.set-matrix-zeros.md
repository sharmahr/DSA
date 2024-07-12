[Set Matrix Zeros](https://leetcode.com/problems/set-matrix-zeroes/description/)

# Intuition
The problem is to set entire rows and columns to zero in a matrix if any element in that row or column is zero. The intuition is to use the first row and first column of the matrix to mark which rows and columns need to be set to zero. We can use two additional variables to indicate if the first row and first column themselves need to be set to zero.

# Approach
1. Initialize variables `rows` and `cols` to store the number of rows and columns in the matrix, respectively.
2. Initialize a boolean variable `firstRow` to indicate if the first row needs to be set to zero.
3. Iterate through each element in the matrix:
   - If the current element is zero, mark the corresponding position in the first row and first column as zero.
   - If the current element is in the first row and is zero, set `firstRow` to true.
4. Iterate through each element in the matrix starting from the second row and second column:
   - If the corresponding position in the first row or first column is marked as zero, set the current element to zero.
5. If the first element `matrix[0][0]` is zero, set the entire first column to zero.
6. If `firstRow` is true, set the entire first row to zero.

# Complexity
- Time complexity: $O(m \times n)$, where $m$ and $n$ are the number of rows and columns in the matrix, respectively.
  - We iterate through each element in the matrix twice.
- Space complexity: $O(1)$
  - We use only a constant amount of extra space for the `firstRow` variable.

# Code
```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        boolean firstRow = false;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    if (i == 0) {
                        firstRow = true;
                    } else {
                        matrix[i][0] = 0;
                    }
                }
            }
        }

        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (matrix[0][0] == 0) {
            for (int i = 0; i < rows; i++) {
                matrix[i][0] = 0;
            }
        }

        if (firstRow) {
            for (int j = 0; j < cols; j++) {
                matrix[0][j] = 0;
            }
        }
    }
}
```