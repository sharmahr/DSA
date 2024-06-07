[Kruskal's Algorithm](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

# Intuition
The problem requires finding the minimum spanning tree (MST) of a weighted undirected graph. The intuition is to use Kruskal's algorithm, which starts by sorting all the edges in ascending order of their weights and then greedily selects the minimum weight edge that does not create a cycle until all vertices are connected.

Note to remember: Kruskal's algorithm builds the MST by adding the minimum weight edge at each step, ensuring that no cycle is formed in the process.

# Approach
1. Create a list `edges` to store all the edges from the adjacency list.

2. Sort the edges in ascending order of their weights.

3. Create a disjoint set data structure using an array `parent` to keep track of the connected components.

4. Initialize variables `mstWeight` to store the total weight of the MST and `edgesAdded` to keep track of the number of edges added to the MST.

5. Iterate through the sorted edges:
   - For each edge `(u, v)` with weight `weight`:
     - Find the parent of vertices `u` and `v` using the `find` function.
     - If the parents are different, it means adding the edge will not create a cycle:
       - Add the weight of the edge to `mstWeight`.
       - Increment `edgesAdded`.
       - Union the sets containing `u` and `v` by updating their parents.
     - If `edgesAdded` equals `V-1`, it means we have found the MST, so we can break the loop.

6. Return the total weight of the MST stored in `mstWeight`.

# Complexity
- Time complexity:
  - Sorting the edges takes $O(E \log E)$ time, where $E$ is the number of edges in the graph.
  - The `find` and union operations take $O(\log V)$ time in the worst case, where $V$ is the number of vertices in the graph.
  - Overall, the time complexity is $O(E \log E)$ or $O(E \log V)$ (since $E$ can be at most $V^2$).
* Space complexity:
  - The space complexity is $O(E)$ to store the `edges` list and $O(V)$ for the `parent` array.

# Code
```java
class Solution {
    static int spanningTree(int V, int E, List<List<int[]>> adj) {
        // Create a list to store all the edges
        List<int[]> edges = new ArrayList<>();

        // Add all the edges from the adjacency list to the edges list
        for (int i = 0; i < V; i++) {
            for (int[] edge : adj.get(i)) {
                int u = i;
                int v = edge[0];
                int weight = edge[1];
                edges.add(new int[]{u, v, weight});
            }
        }

        // Sort the edges in ascending order of their weights
        Collections.sort(edges, (a, b) -> a[2] - b[2]);

        // Create a disjoint set data structure
        int[] parent = new int[V];
        for (int i = 0; i < V; i++) {
            parent[i] = i;
        }

        int mstWeight = 0;
        int edgesAdded = 0;

        // Iterate through the sorted edges
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];

            // Find the parent of u and v using the find function
            int parentU = find(parent, u);
            int parentV = find(parent, v);

            // If the parents are different, it means adding the edge will not create a cycle
            if (parentU != parentV) {
                // Add the edge to the MST
                mstWeight += weight;
                edgesAdded++;

                // Union the sets containing u and v
                parent[parentU] = parentV;
            }

            // If we have added V-1 edges, we have found the MST
            if (edgesAdded == V - 1) {
                break;
            }
        }

        return mstWeight;
    }

    // Find function to find the parent of a vertex with path compression
    static int find(int[] parent, int vertex) {
        if (parent[vertex] != vertex) {
            parent[vertex] = find(parent, parent[vertex]);
        }
        return parent[vertex];
    }
}
```