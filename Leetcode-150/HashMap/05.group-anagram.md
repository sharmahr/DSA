[Group Anagrams](https://leetcode.com/problems/group-anagrams/)

# Intuition
To group anagrams together, we can use a hashmap where the key is a sorted version of each word, and the value is a list of words that are anagrams of each other. By sorting each word, anagrams will have the same sorted representation and will be grouped together in the hashmap.

To remember this solution, think of using a hashmap with sorted words as keys and lists of anagrams as values.

# Approach
1. Create an empty hashmap called `map` to store the sorted words as keys and lists of anagrams as values.
2. Iterate through each word in the input array `strs`:
   - Convert the word to a character array `chars`.
   - Sort the character array `chars`.
   - Create a new string `sortedWord` from the sorted character array.
   - If the `sortedWord` is not already present in the `map`:
     - Create a new empty list and add it to the `map` with `sortedWord` as the key.
   - Add the original word to the list associated with the `sortedWord` in the `map`.
3. Return a new list containing all the values (lists of anagrams) from the `map`.

# Complexity
- Time complexity: $O(n * k * \log k)$, where $n$ is the number of words in the input array `strs`, and $k$ is the maximum length of a word. We iterate through each word in the array, and for each word, we sort its characters, which takes $O(k * \log k)$ time.
- Space complexity: $O(n * k)$, where $n$ is the number of words in the input array `strs`, and $k$ is the maximum length of a word. In the worst case, all words are distinct anagrams, and we store them all in the hashmap.

# Code
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        
        for (String word : strs) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sortedWord = new String(chars);
            
            if (!map.containsKey(sortedWord)) {
                map.put(sortedWord, new ArrayList<>());
            }
            
            map.get(sortedWord).add(word);
        }
        
        return new ArrayList<>(map.values());
    }
}
```