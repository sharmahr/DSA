[Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

# Intuition
The problem of designing a data structure for adding words and searching for words with wildcards can be solved using a Trie (prefix tree) data structure. The intuition is to store the words in a Trie, where each node represents a character and the end of a word is marked with a special flag. To handle wildcards ('.') during the search, we need to modify the search function to explore all possible paths in the Trie when encountering a wildcard.

# Approach
1. Define a `TrieNode` class to represent each node in the Trie. Each node contains:
   - An array `children` of size 26 to store the child nodes, where each index represents a lowercase letter (a-z).
   - A boolean `isEndOfWord` to mark the end of a word.
2. Initialize the Trie with a root node in the constructor.
3. To add a word to the Trie:
   - Start from the root node.
   - Iterate through each character of the word:
     - Calculate the index of the character by subtracting 'a' from it (assuming lowercase letters only).
     - If the child node at the calculated index is null, create a new `TrieNode` and assign it to that index.
     - Move to the child node.
   - After iterating through all characters, mark the last node as the end of the word by setting `isEndOfWord` to true.
4. To search for a word in the Trie (with wildcards):
   - Define a recursive function `searchInNode` that takes the word, current index, and current node as parameters.
   - Base case: If the current index is equal to the length of the word, return the value of `isEndOfWord` of the current node.
   - If the current character is a wildcard ('.'):
     - Iterate through all the child nodes of the current node.
     - Recursively call `searchInNode` for each non-null child node with the updated index.
     - If any recursive call returns true, return true.
     - If no recursive call returns true, return false.
   - If the current character is a letter:
     - Calculate the index of the character by subtracting 'a' from it.
     - If the child node at the calculated index is null, return false.
     - Recursively call `searchInNode` with the updated index and the child node.
5. The `search` function initializes the search by calling `searchInNode` with the word, starting index 0, and the root node.

# Complexity
- Time complexity:
  - Insertion: O(L), where L is the length of the word being inserted.
  - Search: O(M), where M is the number of nodes in the Trie that match the search word. In the worst case, when the search word consists of only wildcards, the search could explore all nodes in the Trie.
- Space complexity: O(N * L), where N is the number of words inserted and L is the average length of the words. In the worst case, when all words have distinct characters, the Trie will have N * L nodes.

# Code
```java
class WordDictionary {

    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        boolean isEndOfWord = false;
    }

    TrieNode root;

    public WordDictionary() {
        root = new TrieNode();
    }
    
    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index];
        }
        node.isEndOfWord = true;
    }
    
    // search for a word in the data structure, '.' can match any letter
    public boolean search(String word) {
        return searchInNode(word, 0, root);
    }

    private boolean searchInNode(String word, int index, TrieNode node) {
        if (index == word.length()) {
            return node.isEndOfWord;
        }

        char c = word.charAt(index);
        if (c == '.') {
            for (TrieNode child : node.children) {
                if (child != null && searchInNode(word, index + 1, child)) {
                    return true;
                }
            }
            return false;
        } else {
            int childIndex = c - 'a';
            TrieNode child = node.children[childIndex];
            if (child == null) {
                return false;
            }
            return searchInNode(word, index + 1, child);
        }
    }
}
```