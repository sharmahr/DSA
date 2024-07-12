[Word Search 2](https://leetcode.com/problems/word-search-ii/description/)

# Intuition
The problem of finding all words in a board that can be formed by a list of given words can be solved using a combination of a Trie data structure and depth-first search (DFS). The intuition is to build a Trie with the given words and then perform DFS on the board to explore all possible paths and check if any word from the Trie can be formed along the path.

# Approach
1. Define a `TrieNode` class to represent each node in the Trie. Each node contains:
   - An array `children` of size 26 to store the child nodes, where each index represents a lowercase letter (a-z).
   - A string `word` to store the complete word if it ends at the current node.
2. Define a `Trie` class to represent the Trie data structure. It contains:
   - A `root` node of type `TrieNode`.
   - An `insert` method to insert a word into the Trie.
   - A `getRoot` method to get the root node of the Trie.
3. In the `findWords` method:
   - Create a Trie and insert all the given words into it.
   - Initialize an empty set `result` to store the found words.
   - Iterate through each cell in the board:
     - Perform DFS starting from the current cell by calling the `dfs` method with the board, current cell coordinates, root node of the Trie, and the `result` set.
   - Convert the `result` set to a list and return it.
4. In the `dfs` method:
   - Get the character at the current cell.
   - If the current cell is already visited (marked as '#') or the current character does not exist in the Trie, return (base case).
   - Move to the child node corresponding to the current character in the Trie.
   - If the current node represents the end of a word, add the word to the `result` set.
   - Mark the current cell as visited by changing its value to '#'.
   - Recursively explore the neighboring cells (up, down, left, right) by calling `dfs` with the updated coordinates.
   - Restore the original character in the current cell (backtrack).

# Complexity
- Time complexity: O(M * (4 * 3^(L-1))), where M is the number of cells in the board, L is the maximum length of words, and the factor of 4 is for exploring the four directions in DFS. In the worst case, for each cell, we explore all possible paths of length L, and at each step, we have at most 3 directions to choose from (excluding the direction we came from).
- Space complexity: O(N), where N is the total number of letters in the Trie. In the worst case, all words are inserted into the Trie without any overlapping prefixes.

# Code
```java
class Solution {
    int[][] directions = {{0,1},{0,-1},{1,0},{-1,0}};
    
    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        String word;
    }

    class Trie {
        TrieNode root;

        Trie(){
            this.root = new TrieNode();
        }

        void insert(String word){
            TrieNode node = root;
            for(char c : word.toCharArray()){
                int index = c - 'a';
                if(node.children[index] == null){
                    node.children[index] = new TrieNode();
                }
                node = node.children[index];
            }
            // mark the end of the word
            node.word = word;
        }

        TrieNode getRoot(){
            return this.root;
        }
    }

    public List<String> findWords(char[][] board, String[] words) {
        Trie trie = new Trie();
        for(String word: words){
            trie.insert(word);
        }

        Set<String> result = new HashSet<String>(); // storing the result
        int x = board.length, y = board[0].length;
        for(int i=0;i<x;i++){
            for(int j=0;j<y;j++){
                dfs(board, i, j, trie.getRoot(), result);
            }
        }

        return new ArrayList<>(result);
    }

    void dfs(char[][] board, int row, int col, TrieNode node, Set<String> result){
        char c = board[row][col];

        if(c == '#' || node.children[c-'a'] == null){
            return; // base case if the node is already visited or the word does not exist
        }

        node = node.children[c-'a'];
        if(node.word != null){
            // add the word to the result
            result.add(node.word);
        }

        board[row][col] = '#'; //mark the cell as visited

        for(int k=0;k<4;k++){
            int x = row + directions[k][0];
            int y = col + directions[k][1];

            if(x >=0 && x < board.length && y >= 0 && y < board[0].length && board[x][y] != '#'){
                dfs(board, x, y, node, result);
            }
        }

        board[row][col] = c; // restore the cell
    }
}
```