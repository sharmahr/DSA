[Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

# Intuition
To find the itinerary in lexical order, we can use a depth-first search (DFS) approach. We can represent the tickets as a graph, where each airport is a node, and each ticket is an edge. We can use a map to store the graph, with the source airport as the key and a priority queue of destination airports as the value. The priority queue ensures that the destinations are visited in lexical order.

# Approach
1. Create an empty list `result` to store the final itinerary.
2. Create a map `map` to represent the graph, where the key is the source airport, and the value is a priority queue of destination airports.
3. Iterate through each ticket in the `tickets` list and add the destination airport to the priority queue of the corresponding source airport in the `map`.
4. Create a stack `stack` to perform the DFS and push the starting airport "JFK" onto the stack.
5. While the stack is not empty:
   - Peek at the top element `next` of the stack.
   - If the priority queue of destinations for the `next` airport is not empty:
     - Push the next destination airport from the priority queue onto the stack.
   - Else:
     - Pop the `next` airport from the stack and add it to the front of the `result` list.
6. Return the `result` list containing the final itinerary.

# Complexity
- Time complexity: O(N log N)
  - N is the number of tickets.
  - Building the graph using the map and priority queues takes O(N log N) time, as each insertion into the priority queue takes O(log N) time.
  - The DFS traversal visits each ticket once, and the operation to add an airport to the front of the result list takes O(1) time.
- Space complexity: O(N)
  - The map used to represent the graph can contain at most N entries, one for each source airport.
  - The stack used for DFS can contain at most N airports.
  - The result list can contain at most N+1 airports (including the starting airport).

# Code
```java
class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        List<String> result = new LinkedList<>();
        Map<String, PriorityQueue<String>> map = new HashMap<>(); // Represent the graph as a map
        Stack<String> stack = new Stack<>(); // DFS stack
        
        for (List<String> ticket : tickets) {
            map.computeIfAbsent(ticket.get(0), k -> new PriorityQueue<>()).add(ticket.get(1));
        }

        stack.push("JFK");
        while (!stack.isEmpty()) {
            String next = stack.peek();

            if (map.getOrDefault(next, new PriorityQueue<>()).isEmpty()) {
                result.add(0, stack.pop()); // Add the airport to the front of the result list
            } else {
                stack.push(map.get(next).poll()); // Push the next destination airport onto the stack
            }
        }
        
        return result;
    }
}
```