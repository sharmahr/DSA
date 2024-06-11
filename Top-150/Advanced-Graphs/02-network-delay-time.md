[Network Delay Time](https://leetcode.com/problems/network-delay-time/)

# Intuition
To find the network delay time, we can use Dijkstra's algorithm to calculate the shortest distance from the starting node to all other nodes. The network delay time will be the maximum distance among all reachable nodes.

# Approach
1. Create an adjacency list to represent the graph using the given `times` array.
2. Initialize a min-heap (priority queue) to store the nodes with their distances from the starting node. The node with the smallest distance will be at the top of the heap.
3. Initialize a distance array to store the shortest distance to each node. Set all distances to infinity except for the starting node, which has a distance of 0.
4. Initialize a boolean array to keep track of visited nodes.
5. While the min-heap is not empty:
   - Extract the node with the smallest distance from the heap.
   - If the node is already visited, continue to the next iteration.
   - Mark the node as visited.
   - For each neighbor of the current node:
     - If the neighbor is not visited and the distance to the neighbor through the current node is smaller than the current distance to the neighbor:
       - Update the distance to the neighbor.
       - Add the neighbor and its updated distance to the min-heap.
6. Find the maximum distance among all nodes. If any node has a distance of infinity, it means it is not reachable, so return -1.
7. Return the maximum distance as the network delay time.

# Complexity
- Time complexity: O((E + V) * log(V))
  - E is the number of edges (length of the `times` array).
  - V is the number of nodes.
  - Building the adjacency list takes O(E) time.
  - Dijkstra's algorithm uses a min-heap, and each operation (insertion and extraction) takes O(log(V)) time. In the worst case, all edges are processed, resulting in O((E + V) * log(V)) time complexity.
- Space complexity: O(E + V)
  - The adjacency list requires O(E) space to store the edges.
  - The min-heap and the distance array require O(V) space.

# Code
```java
import java.util.*;

class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        // Create the adjacency list
        List<List<int[]>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] time : times) {
            graph.get(time[0]).add(new int[]{time[1], time[2]});
        }

        // Min-heap to get the node with the smallest distance
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        minHeap.add(new int[]{k, 0});

        // Distance array to store the shortest distance to each node
        int[] dist = new int[n + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[k] = 0;

        // Set to keep track of visited nodes
        boolean[] visited = new boolean[n + 1];

        while (!minHeap.isEmpty()) {
            int[] current = minHeap.poll();
            int node = current[0];
            int time = current[1];

            if (visited[node]) continue;
            visited[node] = true;

            for (int[] neighbor : graph.get(node)) {
                int nextNode = neighbor[0];
                int travelTime = neighbor[1];

                if (!visited[nextNode] && dist[node] + travelTime < dist[nextNode]) {
                    dist[nextNode] = dist[node] + travelTime;
                    minHeap.add(new int[]{nextNode, dist[nextNode]});
                }
            }
        }

        // Find the maximum distance to all nodes
        int maxTime = 0;
        for (int i = 1; i <= n; i++) {
            if (dist[i] == Integer.MAX_VALUE) return -1;
            maxTime = Math.max(maxTime, dist[i]);
        }

        return maxTime;
    }
}
```