[Partition Labels](https://leetcode.com/problems/partition-labels/description/)

# Intuition
The problem of partitioning a string into as many parts as possible such that each letter appears in at most one part can be solved using a greedy approach. The intuition is to find the last occurrence of each character in the string and use that information to determine the partition points. We can use a hashmap to store the last occurrence index of each character. Then, we iterate through the string and update the last occurrence index whenever we encounter a character. When we reach the last occurrence index of a character, we have found a partition point.

# Approach
1. Build a hashmap `map` to store the last occurrence index of each character in the string.
2. Initialize an empty list `result` to store the lengths of the partitions.
3. Initialize two pointers, `i` and `last`, both pointing to the start of the string.
4. While `i` is less than the length of the string:
   - Initialize a variable `count` to 0 to keep track of the length of the current partition.
   - Update `last` to the maximum value between the current `last` and the last occurrence index of the character at index `i` in the hashmap.
   - While `i` is less than or equal to `last`:
     - Update `last` to the maximum value between the current `last` and the last occurrence index of the character at index `i` in the hashmap.
     - Increment `i` by 1 and `count` by 1.
   - Add `count` to the `result` list, representing the length of the current partition.
5. Return the `result` list containing the lengths of the partitions.

# Complexity
- Time complexity: O(n), where n is the length of the string. We iterate through the string twice, once to build the hashmap and once to find the partitions.
- Space complexity: O(1) since the hashmap will store at most 26 characters (assuming lowercase English letters only) and the result list will store the lengths of the partitions, which is at most n/2.

# Code
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        // build a hashmap for storing the character and the last know index
        Map<Character, Integer> map = new HashMap<>();
        for(int i=0; i<s.length(); i++){
            map.put(s.charAt(i), i);
        }

        List<Integer> result = new ArrayList<>();
        int i = 0;
        int last = 0;
        while(i < s.length()){
            int count = 0;
            last = Math.max(last, map.get(s.charAt(i)));
            while(i<=last){
                last = Math.max(last, map.get(s.charAt(i)));
                i += 1;
                count += 1;
            }
            result.add(count);
        }

        return result;
    }
}
```