[Word Ladder](https://leetcode.com/problems/word-ladder/description/)

# Intuition
To find the shortest transformation sequence from `beginWord` to `endWord`, we can use a breadth-first search (BFS) approach. We can treat each word as a node in a graph, and an edge exists between two words if they differ by exactly one letter. By performing BFS starting from `beginWord`, we can find the shortest path to reach `endWord`.

# Approach
1. Create an adjacency list representation of the graph using the given `wordList`.
   - For each word in the `wordList`, generate all possible patterns by replacing each letter with a wildcard character ('*').
   - Map each pattern to a list of words that match that pattern.
2. Add `beginWord` to the `wordList` to ensure it is included in the graph.
3. Initialize a queue and a set to keep track of visited words.
4. Enqueue `beginWord` into the queue and mark it as visited.
5. Initialize a variable `step` to 1 to represent the length of the transformation sequence.
6. Perform BFS using the queue:
   - While the queue is not empty:
     - Increment `step` by 1.
     - Get the size of the queue (`size`) to process all words at the current level.
     - For each word in the queue:
       - Generate all possible patterns by replacing each letter with a wildcard character ('*').
       - For each pattern, retrieve the list of words that match that pattern from the adjacency list.
       - For each word in the list:
         - If the word is equal to `endWord`, return `step` as the shortest transformation sequence length.
         - If the word has already been visited, skip it.
         - Enqueue the word into the queue and mark it as visited.
7. If the BFS completes without finding `endWord`, return 0 to indicate that no transformation sequence exists.

# Complexity
- Time complexity: O(N * M^2)
  - N is the number of words in the `wordList`.
  - M is the length of each word.
  - Generating the adjacency list takes O(N * M^2) time, as we iterate over each word and generate all possible patterns.
  - The BFS traversal takes O(N * M) time, as we visit each word and its neighbors.
- Space complexity: O(N * M)
  - The adjacency list representation of the graph requires O(N * M) space to store the patterns and their corresponding words.
  - The queue and the visited set can contain at most N words, requiring O(N) space.

# Code
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Map<String, List<String>> adjList = new HashMap<>();
        wordList.add(beginWord);
        
        for (String word : wordList) {
            StringBuilder sb = null;
            for (int i = 0; i < word.length(); i++) {
                sb = new StringBuilder(word);
                sb.setCharAt(i, '*');
                String pattern = sb.toString();
                List<String> neighbors = adjList.getOrDefault(pattern, new ArrayList<>());
                neighbors.add(word);
                adjList.put(pattern, neighbors);
            }
        }
        
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        
        queue.offer(beginWord);
        visited.add(beginWord);
        
        int step = 1;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String currentWord = queue.poll();
                
                if (currentWord.equals(endWord)) {
                    return step;
                }
                
                StringBuilder sb = null;
                for (int j = 0; j < currentWord.length(); j++) {
                    sb = new StringBuilder(currentWord);
                    sb.setCharAt(j, '*');
                    String pattern = sb.toString();
                    
                    for (String neighbor : adjList.getOrDefault(pattern, new ArrayList<>())) {
                        if (!visited.contains(neighbor)) {
                            queue.offer(neighbor);
                            visited.add(neighbor);
                        }
                    }
                }
            }
            step++;
        }
        
        return 0;
    }
}
```