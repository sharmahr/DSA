[Longest Substring without repeating characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

# Intuition
The problem is to find the length of the longest substring without repeating characters in a given string. The intuition is to use a sliding window technique, where we maintain a set of characters seen so far in the current substring, and expand or shrink the window as needed to ensure that there are no repeating characters.

# Approach
1. Initialize two pointers, `left` and `right`, to represent the sliding window.
2. Initialize a set `charSet` to store the characters in the current substring.
3. Initialize a variable `maxLength` to keep track of the maximum length of the substring without repeating characters.
4. Move the `right` pointer to the right, and for each character:
   a. If the character is not in the `charSet`, add it to the set and update `maxLength` to be the maximum of `maxLength` and the length of the current substring (`right - left + 1`).
   b. If the character is in the `charSet`, move the `left` pointer to the right until the repeating character is removed from the current substring, and remove the characters from the `charSet` accordingly.
5. Return `maxLength` as the length of the longest substring without repeating characters.

# Complexity
- Time complexity: O(n)
* Space complexity: O(min(m, n))

Where `n` is the length of the input string, and `m` is the size of the character set (in this case, 128 for ASCII characters).

# Code
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLength = 0;
        Set<Character> charSet = new HashSet<>();
        int left = 0;
        
        for (int right = 0; right < n; right++) {
            if (!charSet.contains(s.charAt(right))) {
                charSet.add(s.charAt(right));
                maxLength = Math.max(maxLength, right - left + 1);
            } else {
                while (charSet.contains(s.charAt(right))) {
                    charSet.remove(s.charAt(left));
                    left++;
                }
                charSet.add(s.charAt(right));
            }
        }
        
        return maxLength;
    }
}
```