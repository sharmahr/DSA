[Euler Circuit and Path](https://www.geeksforgeeks.org/problems/euler-circuit-and-path/1)

# Intuition
To determine if a graph contains an Eulerian circuit or an Eulerian path, we can use the following properties:
- An Eulerian circuit exists if all vertices have an even degree.
- An Eulerian path exists if exactly two vertices have an odd degree.

Note to remember: The degree of a vertex is the number of edges incident to it. In an undirected graph, the degree of a vertex is equal to the size of its adjacency list.

# Approach
1. Initialize a variable `oddDegreeVertices` to count the number of vertices with an odd degree.

2. Iterate over all the vertices in the graph.

3. For each vertex `v`, check the size of its adjacency list `adj[v]`. If the size is odd, increment the `oddDegreeVertices` count.

4. After iterating over all the vertices, check the value of `oddDegreeVertices`:
   - If `oddDegreeVertices` is 0, it means all vertices have an even degree. In this case, the graph contains an Eulerian circuit, so return 2.
   - If `oddDegreeVertices` is 2, it means exactly two vertices have an odd degree. In this case, the graph contains an Eulerian path, so return 1.
   - If `oddDegreeVertices` is neither 0 nor 2, it means the graph is neither an Eulerian circuit nor an Eulerian path, so return 0.

# Complexity
- Time complexity: $O(V+E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - We iterate over all the vertices and their adjacent edges once.
* Space complexity: $O(V)$
  - The space required to store the adjacency list is proportional to the number of vertices V.

# Code
```java
class Solution {
    public int isEulerCircuit(int V, List<Integer>[] adj) {
        // Count the number of vertices with odd degree
        int oddDegreeVertices = 0;

        // Iterate over all vertices
        for (int v = 0; v < V; v++) {
            // If the degree of the vertex is odd, increment the count
            if (adj[v].size() % 2 != 0) {
                oddDegreeVertices++;
            }
        }

        // If all vertices have even degree, it's an Eulerian circuit
        if (oddDegreeVertices == 0) {
            return 2;
        }
        // If exactly two vertices have odd degree, it's an Eulerian path
        else if (oddDegreeVertices == 2) {
            return 1;
        }
        // Otherwise, it's neither an Eulerian circuit nor an Eulerian path
        else {
            return 0;
        }
    }
}
```