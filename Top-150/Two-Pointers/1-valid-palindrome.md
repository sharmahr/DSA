[Valid Palidrome](https://leetcode.com/problems/valid-palindrome/description/)

# Intuition
The problem asks to determine whether a given string is a palindrome after removing non-alphanumeric characters and ignoring the case. The intuition is to use two pointers, one starting from the beginning and the other from the end of the string, and move them inwards while skipping non-alphanumeric characters. If the characters at the two pointers are different (after converting them to the same case), the string is not a palindrome.

# Approach
1. Check if the input string is empty. If so, return true as an empty string is considered a palindrome.
2. Initialize two pointers, `start` and `last`, pointing to the first and last indices of the string, respectively.
3. While `start` is less than or equal to `last`, do the following:
   a. Move `start` forward until it points to an alphanumeric character.
   b. Move `last` backward until it points to an alphanumeric character.
   c. If the characters at `start` and `last` are different (after converting them to the same case), return false.
   d. Otherwise, move `start` forward and `last` backward.
4. If the loop completes without returning false, the string is a palindrome, so return true.

# Complexity
- Time complexity: O(n), where n is the length of the input string. In the worst case, we need to check every character in the string.
- Space complexity: O(1), as we are using only a constant amount of extra space for the pointers and temporary variables.

# Code
```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s.isEmpty()) {
            return true;
        }
        int start = 0;
        int last = s.length() - 1;
        while(start <= last) {
            char currFirst = s.charAt(start);
            char currLast = s.charAt(last);
            if (!Character.isLetterOrDigit(currFirst)) {
                start++;
            } else if(!Character.isLetterOrDigit(currLast)) {
                last--;
            } else {
                if (Character.toLowerCase(currFirst) != Character.toLowerCase(currLast)) {
                    return false;
                }
                start++;
                last--;
            }
        }
        return true;
    }
}
```