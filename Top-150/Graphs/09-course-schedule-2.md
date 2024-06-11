[Course Schedule 2](https://leetcode.com/problems/course-schedule-ii/)

# Intuition
To find a valid course schedule, we can use topological sorting. If there is a cycle in the dependency graph, it means that there is no valid course schedule. We can perform a depth-first search (DFS) on the graph and check for cycles. If no cycles are detected, we can generate a valid course schedule by adding the courses to a stack in the order of completion.

# Approach
1. Create an adjacency list representation of the graph using the given prerequisites.
2. Initialize a stack to store the course schedule and two boolean arrays, `visited` and `inRecursion`, to keep track of visited courses and courses in the current recursion stack.
3. Iterate through each course and perform DFS on unvisited courses.
4. During DFS:
   - If the current course is already in the recursion stack, it means a cycle is detected, so return `true`.
   - If the current course is already visited, return `false`.
   - Mark the current course as visited and in the recursion stack.
   - Iterate through the adjacent courses of the current course and perform DFS on them.
   - If any of the adjacent courses return `true`, it means a cycle is detected, so return `true`.
   - After processing all adjacent courses, remove the current course from the recursion stack and push it onto the stack.
5. If DFS completes without detecting any cycles, convert the stack to the result array and return it.
6. If a cycle is detected during DFS, return an empty array.

# Complexity
- Time complexity: O(V + E)
  - V is the number of courses (vertices) and E is the number of prerequisites (edges) in the graph.
  - The DFS traversal visits each course (vertex) once and processes each prerequisite (edge) once.
- Space complexity: O(V)
  - The adjacency list representation of the graph requires O(V) space to store the courses.
  - The `visited` and `inRecursion` arrays also require O(V) space.
  - The recursion stack in DFS can go up to a depth of V in the worst case.

# Code
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // Adjacency list representation of the graph
        List<List<Integer>> list = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            list.add(new ArrayList<>());
        }
        for (int[] prerequisite : prerequisites) {
            int course = prerequisite[0];
            int prereq = prerequisite[1];
            list.get(prereq).add(course); // Correct edge direction
        }

        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[numCourses];
        boolean[] inRecursion = new boolean[numCourses];

        // Check for cycles and perform DFS for each course
        for (int i = 0; i < numCourses; i++) {
            if (!visited[i] && isCyclic(list, visited, inRecursion, stack, i)) {
                return new int[0]; // If a cycle is detected, return an empty array
            }
        }

        // Convert the stack to the result array
        int[] result = new int[numCourses];
        for (int i = 0; i < numCourses; i++) {
            result[i] = stack.pop();
        }
        return result;
    }

    boolean isCyclic(List<List<Integer>> list, boolean[] visited, boolean[] inRecursion, Stack<Integer> stack, int u) {
        if (inRecursion[u]) return true; // cycle detected
        if (visited[u]) return false;

        visited[u] = true;
        inRecursion[u] = true;

        for (int v : list.get(u)) {
            if (isCyclic(list, visited, inRecursion, stack, v)) {
                return true;
            }
        }

        inRecursion[u] = false; // removing the node from the recursion stack
        stack.push(u); // push the node to stack after processing all its adjacent nodes
        return false;
    }
}
```