## Graph
#### Easy
#### Medium
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [Number Of Islands](https://leetcode.com/problems/number-of-islands/description/) |  Depth-first search (DFS) starting from each unvisited '1' cell and mark all the connected '1' cells as visited. The number of times the DFS is initiated will give the count of islands. | Solution |
| [Max Area Of Island](https://leetcode.com/problems/max-area-of-island/description/) | Perform a depth-first search (DFS) starting from each unvisited cell with a value of 1. During the DFS, we can count the number of cells that belong to the current island and update the maximum area if necessary. | Row 2 |
| [Clone Graph](https://leetcode.com/problems/clone-graph/description/) | Perform a depth-first search (DFS) traversal of the graph and create a cloned node for each visited node. We can use a hash map to keep track of the mapping between the original nodes and their cloned counterparts to avoid creating duplicate clones. | Row 3, Cell 3 |
| [Count Sub Islands](https://leetcode.com/problems/count-sub-islands/description/) | Perform a depth-first search (DFS) on grid2 and check if each island in grid2 is also an island in grid1 | Row 3, Cell 3 |
| [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/description/) | Perform a depth-first search (DFS) from the boundary cells of the matrix and mark the cells that can reach the respective ocean. Then, find the cells that are marked as reachable to both oceans. | Row 3, Cell 3 |
| [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/description/) | Perform a depth-first search (DFS) starting from the 'O' cells on the borders and mark all the connected 'O' cells as a special character (e.g., ''). After the DFS, all the remaining 'O' cells that are not marked as '' are the ones that need to be captured and changed to 'X'. | Row 3, Cell 3 |
| [Snakes and Ladders](https://leetcode.com/problems/snakes-and-ladders/description/) | Use a breadth-first search (BFS) algorithm to explore all possible moves from each square and find the shortest path to the target square. | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |