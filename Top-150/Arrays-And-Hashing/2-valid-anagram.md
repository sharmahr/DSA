[Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

# Intuition
To determine if two strings are anagrams, we need to check if they contain the same characters with the same frequency. One approach is to count the frequency of each character in both strings and compare them. If the frequency counts match, the strings are anagrams.

To remember this solution, think of using a hashmap to store the character frequencies and comparing them.

# Approach
1. Create a helper function `getLetterFrequency` that takes a string `s` and returns a hashmap containing the frequency count of each character in `s`.
2. Call `getLetterFrequency` with the first string `s` to get the frequency count of its characters.
3. Iterate through each character `c` in the second string `t`:
  - Get the frequency count of `c` from the hashmap using `smap.getOrDefault(c, 0)`.
  - If the count is 0, it means `c` is not present in `s` or its count has already been exhausted, so return `false`.
  - Otherwise, decrement the count of `c` in the hashmap.
4. After the iteration, check if the hashmap is empty by iterating through its values:
  - If any value is greater than 0, it means there are characters in `s` that are not present in `t`, so return `false`.
5. If the iteration completes without returning `false`, it means the strings are anagrams, so return `true`.

# Complexity
- Time complexity: $O(n)$, where $n$ is the length of the strings `s` and `t`. We iterate through each character in both strings once.
- Space complexity: $O(m)$, where $m$ is the number of unique characters in string `s`. In the worst case, all characters in `s` are unique, so the hashmap will store $m$ key-value pairs.

# Code
```java
class Solution {
   public boolean isAnagram(String s, String t) {
       // Create a hashmap to store the character frequencies of string s
       HashMap<Character, Integer> smap = getLetterFrequency(s);
       
       // Iterate through each character in string t
       for (char c : t.toCharArray()) {
           int count = smap.getOrDefault(c, 0);
           if (count == 0) {
               return false; // Character c is not present in s or its count is exhausted
           }
           smap.put(c, count - 1); // Decrement the count of character c in the hashmap
       }
       
       // Check if the hashmap is empty
       for (int value : smap.values()) {
           if (value > 0) {
               return false; // There are characters in s that are not present in t
           }
       }
       
       return true; // The strings are anagrams
   }

   // Helper function to get the character frequency count of a string
   public HashMap<Character, Integer> getLetterFrequency(String s) {
       HashMap<Character, Integer> result = new HashMap<>();
       
       // Iterate through each character in string s
       for (char c : s.toCharArray()) {
           if (result.containsKey(c)) {
               int value = result.get(c);
               result.replace(c, value + 1); // Increment the count of character c
           } else {
               result.put(c, 1); // Add character c to the hashmap with count 1
           }
       }
       
       return result;
   }
}