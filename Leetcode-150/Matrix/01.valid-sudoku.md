[Valid Sudodu](https://leetcode.com/problems/valid-sudoku/description/)

# Intuition
The problem asks us to determine if a given Sudoku board is valid. The intuitive approach is to check the validity of each row, column, and 3x3 block separately. We can use a set to keep track of the numbers encountered in each row, column, and block. If we come across a number that already exists in the corresponding set, it means the Sudoku board is invalid.

# Approach
1. Create an empty set called `seen` to store the numbers encountered in each row, column, and block.
2. Iterate through each cell of the Sudoku board using nested loops, with variables `i` representing the row and `j` representing the column.
3. For each non-empty cell (i.e., not '.'):
   - Extract the number from the cell and store it in the variable `number`.
   - Check if the number already exists in the corresponding row by adding it to the `seen` set with the key `number + " in row " + i`. If the number already exists, return `false` as the Sudoku board is invalid.
   - Check if the number already exists in the corresponding column by adding it to the `seen` set with the key `number + " in column " + j`. If the number already exists, return `false` as the Sudoku board is invalid.
   - Check if the number already exists in the corresponding 3x3 block by adding it to the `seen` set with the key `number + " in block " + i/3 + "-" + j/3`. The block indices are calculated using integer division. If the number already exists, return `false` as the Sudoku board is invalid.
4. If all the checks pass and no invalid condition is found, return `true` as the Sudoku board is valid.

# Complexity
- Time complexity: O(1) since the Sudoku board has a fixed size of 9x9, and the nested loops iterate over a constant number of cells.
- Space complexity: O(1) as the `seen` set will contain a maximum of 9 elements for each row, column, and block, resulting in a constant space usage.

# Code
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set seen = new HashSet();
        for (int i=0; i<9; ++i) {
            for (int j=0; j<9; ++j) {
                char number = board[i][j];
                if (number != '.')
                    if (!seen.add(number + " in row " + i) ||
                        !seen.add(number + " in column " + j) ||
                        !seen.add(number + " in block " + i/3 + "-" + j/3))
                        return false;
            }
        }
        return true;
    }
}
```