[Alien Dictionary](https://neetcode.io/problems/foreign-dictionary)

# Intuition
To find the order of characters in an alien language, we can use topological sorting. We can build a directed graph based on the lexicographic order of the words in the dictionary. Each character represents a node in the graph, and there is an edge from character `a` to character `b` if `a` comes before `b` in the lexicographic order. After building the graph, we can perform a topological sort to determine the order of the characters.

# Approach
1. Create data structures:
   - Create a `graph` using a hash map to represent the adjacency list, where each character is a key, and the corresponding value is a set of characters that come after it in the lexicographic order.
   - Create an `inDegree` hash map to store the in-degree of each character, which represents the number of characters that come before it.
2. Build the graph:
   - Iterate through each pair of adjacent words in the dictionary.
   - Compare the characters at each position of the two words until a difference is found.
   - If a difference is found, add an edge from the character in the first word to the character in the second word, and increment the in-degree of the character in the second word.
   - If no difference is found and the second word is a prefix of the first word, return an empty string as there is no valid ordering.
3. Perform topological sort using BFS:
   - Create a queue and a `StringBuilder` to store the result.
   - Add all characters with in-degree 0 to the queue.
   - While the queue is not empty:
     - Remove a character from the queue and append it to the result.
     - Decrement the in-degree of all its neighboring characters.
     - If the in-degree of a neighboring character becomes 0, add it to the queue.
   - If the length of the result is not equal to the number of characters, return an empty string as there is no valid ordering.
4. Return the result string representing the order of characters in the alien language.

# Complexity
- Time complexity: O(C), where C is the total number of characters in the dictionary.
  - Building the graph requires iterating through each pair of adjacent words and comparing their characters, which takes O(C) time in the worst case.
  - Topological sort using BFS takes O(V + E) time, where V is the number of characters (nodes) and E is the number of edges in the graph. In the worst case, E can be O(C).
- Space complexity: O(C)
  - The `graph` hash map and `inDegree` hash map store the adjacency list and in-degrees of the characters, respectively, which can have at most C entries.
  - The queue used in BFS can contain at most C characters.
  - The `StringBuilder` used to store the result can have a length of at most C.

# Code
```java
class Solution {
    public String alienOrder(String[] words) {
        // Step 1: Create data structures
        Map<Character, Set<Character>> graph = new HashMap<>();
        Map<Character, Integer> inDegree = new HashMap<>();
        for (String word : words) {
            for (char c : word.toCharArray()) {
                graph.putIfAbsent(c, new HashSet<>());
                inDegree.putIfAbsent(c, 0);
            }
        }

        // Step 2: Build the graph
        for (int i = 0; i < words.length - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            int minLength = Math.min(word1.length(), word2.length());
            boolean foundDifference = false;
            for (int j = 0; j < minLength; j++) {
                char char1 = word1.charAt(j);
                char char2 = word2.charAt(j);
                if (char1 != char2) {
                    if (!graph.get(char1).contains(char2)) {
                        graph.get(char1).add(char2);
                        inDegree.put(char2, inDegree.get(char2) + 1);
                    }
                    foundDifference = true;
                    break;
                }
            }
            // Check if word2 is a prefix of word1
            if (!foundDifference && word1.length() > word2.length()) {
                return "";
            }
        }

        // Step 3: Topological sort using BFS
        Queue<Character> queue = new LinkedList<>();
        StringBuilder result = new StringBuilder();

        // Add all nodes with in-degree 0 to the queue
        for (char c : inDegree.keySet()) {
            if (inDegree.get(c) == 0) {
                queue.offer(c);
            }
        }

        while (!queue.isEmpty()) {
            char current = queue.poll();
            result.append(current);
            for (char neighbor : graph.get(current)) {
                inDegree.put(neighbor, inDegree.get(neighbor) - 1);
                if (inDegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        // Check if all characters are in the result
        if (result.length() != inDegree.size()) {
            return "";
        }

        return result.toString();
    }
}
```