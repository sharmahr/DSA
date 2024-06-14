[Valid Parenthesis](https://leetcode.com/problems/valid-parenthesis-string/)

# Intuition
To determine if a string with parentheses and asterisks is valid, we can keep track of the minimum and maximum number of open parentheses needed to make the string valid. The intuition is that for each character in the string, we update the minimum and maximum counts based on the character. If the maximum count becomes negative at any point, it means there are too many closing parentheses, and the string is invalid. If the minimum count becomes negative, we reset it to 0 since we can consider the asterisks as empty. At the end, if the minimum count is 0, it means all open parentheses are matched, and the string is valid.

# Approach
1. Initialize two variables, `minOpen` and `maxOpen`, to keep track of the minimum and maximum number of open parentheses needed, respectively. Both are initialized to 0.
2. Iterate through each character `c` in the string:
   - If `c` is an opening parenthesis '(', increment both `minOpen` and `maxOpen` by 1.
   - If `c` is a closing parenthesis ')', decrement both `minOpen` and `maxOpen` by 1.
   - If `c` is an asterisk '*', decrement `minOpen` by 1 (considering it as empty or closing parenthesis) and increment `maxOpen` by 1 (considering it as an opening parenthesis).
   - If `maxOpen` becomes negative at any point, it means there are too many closing parentheses, and the string is invalid, so return `false`.
   - If `minOpen` becomes negative, reset it to 0 since we can consider the asterisks as empty.
3. After iterating through all characters, check if `minOpen` is 0. If it is, it means all open parentheses are matched, and the string is valid, so return `true`. Otherwise, return `false`.

# Complexity
- Time complexity: O(n), where n is the length of the string. We iterate through each character of the string once.
- Space complexity: O(1) since we only use a constant amount of extra space for the `minOpen` and `maxOpen` variables.

# Code
```java
class Solution {
    public boolean checkValidString(String s) {
        int minOpen = 0; // minimum number of open parentheses needed
        int maxOpen = 0; // maximum number of open parentheses possible
        
        for (char c : s.toCharArray()) {
            if (c == '(') {
                minOpen++;
                maxOpen++;
            } else if (c == ')') {
                minOpen--;
                maxOpen--;
            } else { // c == '*'
                minOpen--; // '*' can be empty or ')'
                maxOpen++; // '*' can be '('
            }
            
            if (maxOpen < 0) { // Too many closing parentheses
                return false;
            }
            
            if (minOpen < 0) { // minOpen should not be negative
                minOpen = 0;
            }
        }
        
        // If minOpen is 0, it means all open parentheses are matched
        return minOpen == 0;
    }
}
```