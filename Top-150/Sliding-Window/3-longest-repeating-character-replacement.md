[Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/description/)

# Intuition
The problem is to find the length of the longest substring in a given string that can be replaced with at most `k` characters to make it a substring of the same characters. The intuition is to use a sliding window technique, where we keep track of the maximum frequency of any character in the current window and the number of characters that need to be replaced to make the substring valid.

# Approach
1. Initialize an array `arr` of size 26 to store the count of each character in the current window.
2. Initialize `res` to keep track of the maximum length of a valid substring, and `max` to store the maximum frequency of any character in the current window.
3. Use two pointers `l` and `r` to represent the sliding window.
4. Iterate through the string `s` using the `r` pointer:
   a. Increment the count of the character `s[r]` in the `arr`.
   b. Update `max` to be the maximum of `max` and the count of `s[r]`.
   c. Calculate the number of characters that need to be replaced in the current window as `r - l + 1 - max`.
   d. If the number of replacements needed is greater than `k`, shrink the window from the left by decrementing the count of `s[l]` in `arr` and moving `l` to the right.
   e. Update `res` to be the maximum of `res` and the length of the current window `r - l + 1`.
5. Return `res` as the length of the longest substring that can be replaced with at most `k` characters.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
Since the array `arr` has a fixed size of 26 (for uppercase English letters), the space complexity is constant.

# Code
```java
class Solution {
    public int characterReplacement(String s, int k) {
        // Initialising an empty array to store the count of the 
        // characters in the given string s
        int[] arr = new int[26];
        int res = 0;
        int max = 0;

        // The left pointer for the sliding window is l AND r is the 
        // right pointer
        int l = 0;
        for (int r = 0; r < s.length(); r++) {
            // Counting the number of each character in the string s
            arr[s.charAt(r) - 'A']++;

            // Checking the character with max number of occurrence
            max = Math.max(max, arr[s.charAt(r) - 'A']);

            // Now we check if our current window is valid or not
            if (r - l + 1 - max > k) { 
            // this means the no. of replacements is more than
            // allowed (k)
                // Decrementing the count of the character which was 
                // at l because it is no longer in the window
                arr[s.charAt(l) - 'A']--;
                l++;
            }

            // The max our window can be
            res = Math.max(res, r - l + 1);
        }

        return res;
    }
}
```