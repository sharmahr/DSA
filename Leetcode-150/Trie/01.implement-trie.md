[Implement Trie Prefix Tree](https://leetcode.com/problems/implement-trie-prefix-tree/description/)

# Intuition
The Trie data structure, also known as a prefix tree, is an efficient way to store and retrieve strings. It allows for fast insertion, search, and prefix matching operations. The intuition behind using a Trie is to represent each character of a string as a node in the tree, with each node potentially having multiple child nodes representing the next characters in the string. By traversing the tree, we can efficiently perform operations like insertion, search, and prefix matching.

# Approach
1. Define a `TrieNode` class to represent each node in the Trie. Each node contains:
   - An array `children` of size 26 to store the child nodes, where each index represents a lowercase letter (a-z).
   - A boolean `isEndOfWord` to mark the end of a word.
2. Initialize the Trie with a root node in the constructor.
3. To insert a word into the Trie:
   - Start from the root node.
   - Iterate through each character of the word:
     - Calculate the index of the character by subtracting 'a' from it (assuming lowercase letters only).
     - If the child node at the calculated index is null, create a new `TrieNode` and assign it to that index.
     - Move to the child node.
   - After iterating through all characters, mark the last node as the end of the word by setting `isEndOfWord` to true.
4. To search for a word in the Trie:
   - Call the helper function `getNode` to traverse the Trie and find the node corresponding to the last character of the word.
   - If the node is not null and `isEndOfWord` is true, return true; otherwise, return false.
5. To check if a prefix exists in the Trie:
   - Call the helper function `getNode` to traverse the Trie and find the node corresponding to the last character of the prefix.
   - If the node is not null, return true; otherwise, return false.
6. The helper function `getNode`:
   - Start from the root node.
   - Iterate through each character of the given word or prefix:
     - Calculate the index of the character by subtracting 'a' from it.
     - If the child node at the calculated index is null, return null (word or prefix not found).
     - Move to the child node.
   - After iterating through all characters, return the last node.

# Complexity
- Time complexity:
  - Insertion: O(L), where L is the length of the word being inserted.
  - Search: O(L), where L is the length of the word being searched.
  - Prefix matching: O(L), where L is the length of the prefix.
- Space complexity: O(N * L), where N is the number of words inserted and L is the average length of the words. In the worst case, when all words have distinct characters, the Trie will have N * L nodes.

# Code
```java
class Trie {

    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        boolean isEndOfWord = false;
    }

    TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    // Insert a node into Trie
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index]; // iterate the nodes
        }
        node.isEndOfWord = true; // mark the end of the word
    }
    
    public boolean search(String word) {
        TrieNode node = getNode(word);
        return node != null && node.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        return getNode(prefix) != null;
    }

    private TrieNode getNode(String word) {
        TrieNode node = root; //start of the traversal
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                return null; // word not found
            }
            node = node.children[index]; // traverse the node
        }
        return node;
    }
}
```