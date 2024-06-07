[Flyod Warshal Algorithm](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1)

# Intuition
The Floyd-Warshall algorithm is used to find the shortest distances between all pairs of vertices in a weighted graph. The algorithm works by considering all vertices as potential intermediate vertices and incrementally updating the shortest distances between pairs of vertices. It can handle negative edge weights but not negative cycles.

Note to remember: The Floyd-Warshall algorithm can be used to solve the all-pairs shortest path problem efficiently.

# Approach
1. Initialize a 2D array `matrix` to represent the adjacency matrix of the graph, where `matrix[i][j]` represents the weight of the edge from vertex `i` to vertex `j`. If there is no direct edge between two vertices, the corresponding entry in the matrix is set to -1.

2. Apply the Floyd-Warshall algorithm:
   - For each intermediate vertex `k` from 0 to `n-1`:
     - For each source vertex `i` from 0 to `n-1`:
       - For each destination vertex `j` from 0 to `n-1`:
         - If there exists a path from `i` to `k` and from `k` to `j`, and the sum of their weights is smaller than the current shortest distance from `i` to `j`, update the shortest distance from `i` to `j` as `matrix[i][k] + matrix[k][j]`.

3. After the algorithm finishes, the `matrix` will be updated with the shortest distances between all pairs of vertices.

# Complexity
- Time complexity:
  - The time complexity of the Floyd-Warshall algorithm is $O(n^3)$, where $n$ is the number of vertices in the graph.
  - The algorithm uses three nested loops, each running from 0 to `n-1`, resulting in a cubic time complexity.
* Space complexity:
  - The space complexity is $O(n^2)$ to store the `matrix` representing the adjacency matrix of the graph.

# Code
```java
class Solution {
    public void shortest_distance(int[][] matrix) {
        int n = matrix.length;

        // Apply Floyd-Warshall algorithm
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (matrix[i][k] != -1 && matrix[k][j] != -1
                            && (matrix[i][j] == -1 || matrix[i][k] + matrix[k][j] < matrix[i][j])) {
                        matrix[i][j] = matrix[i][k] + matrix[k][j];
                    }
                }
            }
        }
    }
}
```