[Course Schedule](https://leetcode.com/problems/course-schedule/)

# Intuition
To determine if it is possible to finish all courses, we need to check if there are any cycles in the dependency graph. If there are no cycles, it means that all courses can be completed. We can use depth-first search (DFS) to detect cycles in the graph.

# Approach
1. Create an adjacency list representation of the graph using the given prerequisites.
2. Initialize two boolean arrays, `visited` and `inRecursion`, to keep track of visited courses and courses in the current recursion stack.
3. Perform DFS for each course:
   - If the current course is already in the recursion stack, it means a cycle is detected, so return `true`.
   - If the current course is already visited, return `false`.
   - Mark the current course as visited and in the recursion stack.
   - Iterate through the prerequisites of the current course and perform DFS on each prerequisite.
   - If any of the prerequisites return `true`, it means a cycle is detected, so return `true`.
   - After processing all prerequisites, remove the current course from the recursion stack.
4. If DFS completes without detecting any cycles, return `true`, indicating that it is possible to finish all courses.

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
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Adjacency list representation of the graph
        List<List<Integer>> list = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            list.add(new ArrayList<>());
        }
        for (int[] prerequisite : prerequisites) {
            int course = prerequisite[0];
            int prereq = prerequisite[1];
            list.get(course).add(prereq);
        }

        boolean[] visited = new boolean[numCourses];
        boolean[] inRecursion = new boolean[numCourses];

        // Perform DFS for each course
        for (int i = 0; i < numCourses; i++) {
            if (!visited[i] && isCyclic(list, visited, inRecursion, i)) {
                return false;
            }
        }
        return true;
    }

    boolean isCyclic(List<List<Integer>> list, boolean[] visited, boolean[] inRecursion, int u) {
        if (inRecursion[u]) return true; // cycle detected
        if (visited[u]) return false;

        visited[u] = true;
        inRecursion[u] = true;

        for (int v : list.get(u)) {
            if (isCyclic(list, visited, inRecursion, v)) {
                return true;
            }
        }

        inRecursion[u] = false; // removing the node from the recursion stack
        return false;
    }
}
```