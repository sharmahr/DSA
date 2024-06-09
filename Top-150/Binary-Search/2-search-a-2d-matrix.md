[Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)

# Intuition
The problem asks to search for a target value in a 2D matrix sorted in both rows and columns. The intuition is to treat the 2D matrix as a single sorted array and perform binary search on it. By flattening the matrix into a 1D array, we can leverage the existing binary search algorithm for sorted arrays.

# Approach
1. Create a 1D array `arr` of size `m * n`, where `m` and `n` are the number of rows and columns in the matrix, respectively.
2. Flatten the 2D matrix into the 1D array `arr` by iterating over each element and storing it in the array.
3. Perform binary search on the flattened array `arr` to find the target value.
   a. Initialize two pointers, `left` and `right`, pointing to the start and end of the array, respectively.
   b. While `left` is less than or equal to `right`, do the following:
      - Calculate the middle index `mid` using `left + (right - left) / 2` to avoid integer overflow.
      - If the element at `mid` is equal to the target, return `true`.
      - If the target is greater than the element at `mid`, update `left` to `mid + 1` to search in the right half of the interval.
      - Otherwise, update `right` to `mid - 1` to search in the left half of the interval.
4. If the loop completes without finding the target, return `false`.

# Complexity
- Time complexity: O(m * n + log(m * n)), where m and n are the number of rows and columns in the matrix, respectively. Flattening the matrix takes O(m * n) time, and binary search on the flattened array takes O(log(m * n)) time.
- Space complexity: O(m * n), as we are using an additional 1D array to store the flattened matrix.

# Code
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int[] arr = new int[m*n];
        int index = 0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                arr[index] = matrix[i][j];
                index += 1;
            }
        }

        int left = 0, right = arr.length-1;
        while(left <= right){
            int mid = left + (right-left)/2;
            if(arr[mid] == target) return true;
            if(target>arr[mid]){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return false;
    }
}
```

While this approach works correctly, it has a potential issue with space complexity. Flattening the entire 2D matrix into a 1D array may not be efficient, especially for large matrices, as it requires additional memory proportional to the size of the matrix.

A more space-efficient approach would be to perform the binary search directly on the 2D matrix without flattening it. This can be achieved by mapping the 2D indices to a 1D index during the binary search process. Here's an alternative solution that follows this approach:

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int left = 0, right = m * n - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int row = mid / n;
            int col = mid % n;
            
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return false;
    }
}
```

In this solution, the time complexity remains O(log(m * n)), but the space complexity is reduced to O(1) since we are not using any additional data structure to store the flattened matrix.