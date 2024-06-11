[Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/description/)

# Intuition
To find the minimum cost to connect all points, we can use Prim's algorithm for minimum spanning tree (MST). We start with any point and gradually expand the tree by adding the point with the minimum cost edge that connects to the existing tree until all points are included.

# Approach
1. Create a priority queue (min-heap) to store the edges as (cost, node) pairs, where cost represents the distance between the node and the existing tree.
2. Initialize the heap with a starting point (e.g., the first point) with a cost of 0.
3. Initialize a set to keep track of the visited nodes and a variable to store the total cost.
4. While the heap is not empty:
   - Extract the edge with the minimum cost from the heap.
   - If the node of the extracted edge is already visited, continue to the next iteration.
   - Otherwise, mark the node as visited and add the cost of the edge to the total cost.
   - Iterate through all the remaining points:
     - If a point is not visited, calculate the distance between the current node and that point.
     - Add the (distance, point) pair to the heap.
5. Return the total cost.

# Complexity
- Time complexity: O(N^2 * log(N))
  - N is the number of points.
  - In the worst case, we need to iterate through all the points for each point, resulting in N^2 iterations.
  - Each iteration involves adding an edge to the heap, which takes O(log(N)) time.
- Space complexity: O(N)
  - The heap can contain at most N edges.
  - The visited set can contain at most N points.

# Code
```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[0] - b[0]); // store the data as (cost, node)
        heap.offer(new int[]{0, 0}); // add the starting point of the nodes
        int length = points.length;
        Set<Integer> visited = new HashSet<>(); // to keep track of the visited nodes
        int cost = 0;

        while (!heap.isEmpty()) {
            int[] edge = heap.poll();
            int edgeCost = edge[0];
            int node = edge[1];

            if (visited.contains(node)) {
                continue; // if the node is already processed
            }

            visited.add(node);
            cost += edgeCost;

            for (int i = 0; i < length; i++) { // process all the remaining nodes
                if (!visited.contains(i)) {
                    int distance = Math.abs(points[i][0] - points[node][0]) + Math.abs(points[i][1] - points[node][1]);
                    heap.offer(new int[]{distance, i});
                }
            }
        }

        return cost;
    }
}
```