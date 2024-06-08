[Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

# Intuition
The problem is to find the minimum window substring of string `s` that contains all characters in string `t`. The intuition is to use a sliding window technique along with two frequency maps to keep track of the characters in `t` and the characters in the current window. We can slide the window and update the frequency maps accordingly to find the minimum window that satisfies the condition.

# Approach
1. Create two frequency maps, `freq_t` and `freq_window`, to store the characters and their frequencies in `t` and the current window, respectively.
2. Initialize `freq_t` by iterating through `t` and incrementing the frequency of each character.
3. Initialize two pointers `left` and `right` to represent the sliding window in `s`.
4. Initialize a variable `count` to keep track of the number of characters in `t` that are not yet found in the current window.
5. Initialize variables `min_len` and `min_start` to store the length and start index of the minimum window, respectively.
6. While `right` is within the bounds of `s`:
   a. Add `s[right]` to `freq_window` and update `count` accordingly.
   b. While `count` is 0 (all characters in `t` are found in the window):
      - Update `min_len` and `min_start` if the current window is smaller than the minimum window found so far.
      - Remove `s[left]` from `freq_window` and update `count` accordingly.
      - Move `left` to the right.
   c. Move `right` to the right.
7. If `min_len` is equal to the maximum possible value (no valid window found), return an empty string. Otherwise, return the substring of `s` starting from `min_start` with length `min_len`.

# Complexity
- Time complexity: O(m + n)
* Space complexity: O(k)
Where `m` and `n` are the lengths of `s` and `t`, respectively, and `k` is the number of unique characters in `t`. The time complexity is O(m + n) because we iterate through both `s` and `t` once. The space complexity is O(k) because the frequency maps store at most `k` unique characters.

# Code
```java
class Solution {
    public String minWindow(String s, String t) {
        if (s == null || t == null || s.length() < t.length()) {
            return "";
        }

        Map<Character, Integer> freq_t = new HashMap<>();
        Map<Character, Integer> freq_window = new HashMap<>();

        // Initialize freq_t
        for (char c : t.toCharArray()) {
            freq_t.put(c, freq_t.getOrDefault(c, 0) + 1);
        }

        int left = 0, right = 0, count = t.length(), min_len = Integer.MAX_VALUE, min_start = 0;

        while (right < s.length()) {
            char c = s.charAt(right);
            if (freq_t.containsKey(c)) {
                freq_window.put(c, freq_window.getOrDefault(c, 0) + 1);
                if (freq_window.get(c) <= freq_t.get(c)) {
                    count--;
                }
            }

            while (count == 0) {
                if (right - left + 1 < min_len) {
                    min_len = right - left + 1;
                    min_start = left;
                }

                char d = s.charAt(left);
                if (freq_t.containsKey(d)) {
                    if (freq_window.get(d) <= freq_t.get(d)) {
                        count++;
                    }
                    freq_window.put(d, freq_window.get(d) - 1);
                }
                left++;
            }
            right++;
        }

        return min_len == Integer.MAX_VALUE ? "" : s.substring(min_start, min_start + min_len);
    }
}
```