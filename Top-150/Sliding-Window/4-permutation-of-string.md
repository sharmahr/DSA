[Permutation in string](https://leetcode.com/problems/permutation-in-string/)

# Intuition
The problem is to determine whether a string `s2` contains a permutation of another string `s1`. The intuition is to use a sliding window technique and compare the frequency of characters in the window with the frequency of characters in `s1`. If the frequencies match, then the window contains a permutation of `s1`.

# Approach
1. Create two arrays `freq1` and `freq2` to store the frequency of characters in `s1` and the current window of `s2`, respectively.
2. Initialize `freq1` by iterating through `s1` and incrementing the corresponding character frequencies.
3. Use two pointers `left` and `right` to represent the sliding window in `s2`.
4. Initialize `freq2` with the first `s1.length()` characters of `s2`.
5. Compare `freq1` and `freq2`. If they are equal, return `true`.
6. Slide the window to the right by incrementing `right` and updating `freq2` accordingly.
7. If the window size is greater than `s1.length()`, slide the window to the left by decrementing `left` and updating `freq2` accordingly.
8. Repeat steps 6 and 7 until `right` reaches the end of `s2`.
9. If no permutation is found, return `false`.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
The space complexity is constant since the arrays `freq1` and `freq2` have a fixed size of 26 (for lowercase English letters).

# Code
```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] freq1 = new int[26];
        int[] freq2 = new int[26];
        
        // Initialize freq1
        for (char c : s1.toCharArray()) {
            freq1[c - 'a']++;
        }
        
        int left = 0;
        int right = 0;
        
        // Initialize freq2 for the first window
        while (right < s1.length() && right < s2.length()) {
            freq2[s2.charAt(right) - 'a']++;
            right++;
        }
        
        if (Arrays.equals(freq1, freq2)) {
            return true;
        }
        
        while (right < s2.length()) {
            // Slide the window to the right
            freq2[s2.charAt(right) - 'a']++;
            right++;
            
            // Slide the window to the left
            if (right - left > s1.length()) {
                freq2[s2.charAt(left) - 'a']--;
                left++;
            }
            
            if (Arrays.equals(freq1, freq2)) {
                return true;
            }
        }
        
        return false;
    }
}
```