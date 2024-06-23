Certainly! As an expert software engineer, I'll help you build an intuition for when to use these algorithms and provide Java code samples for each.

1. Kadane's Algorithm

Use when:
- You need to find the maximum sum contiguous subarray in a one-dimensional array.
- You're dealing with problems involving dynamic programming on arrays.

Example: Maximum Subarray Problem

```java
public class Kadane {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0], maxEndingHere = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
}
```

2. Sliding Window (Fixed Size)

Use when:
- You need to process subarrays or substrings of a fixed length.
- You're looking for a pattern of a fixed size in an array or string.

Example: Find maximum sum subarray of size k

```java
public class FixedSlidingWindow {
    public int maxSumSubarray(int[] arr, int k) {
        int maxSum = 0, windowSum = 0;
        for (int i = 0; i < arr.length; i++) {
            windowSum += arr[i];
            if (i >= k - 1) {
                maxSum = Math.max(maxSum, windowSum);
                windowSum -= arr[i - (k - 1)];
            }
        }
        return maxSum;
    }
}
```

3. Sliding Window (Variable Size)

Use when:
- You need to find the longest/shortest subarray or substring that satisfies a given condition.
- You're dealing with problems involving dynamic size subarrays or substrings.

Example: Longest substring with at most k distinct characters

```java
public class VariableSlidingWindow {
    public int longestSubstringKDistinct(String s, int k) {
        Map<Character, Integer> charCount = new HashMap<>();
        int maxLength = 0, left = 0;
        for (int right = 0; right < s.length(); right++) {
            charCount.put(s.charAt(right), charCount.getOrDefault(s.charAt(right), 0) + 1);
            while (charCount.size() > k) {
                charCount.put(s.charAt(left), charCount.get(s.charAt(left)) - 1);
                if (charCount.get(s.charAt(left)) == 0) charCount.remove(s.charAt(left));
                left++;
            }
            maxLength = Math.max(maxLength, right - left + 1);
        }
        return maxLength;
    }
}
```

4. Two Pointers

Use when:
- You need to search for pairs in a sorted array.
- You're dealing with problems involving reversing or palindromes.
- You need to compare elements from both ends of an array.

Example: Two Sum II - Input array is sorted

```java
public class TwoPointers {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1;
        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                return new int[]{left + 1, right + 1};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[]{-1, -1};
    }
}
```

5. Prefix Sums

Use when:
- You need to calculate the sum of elements in a range quickly.
- You're dealing with problems involving cumulative sums or differences.

Example: Range Sum Query - Immutable

```java
public class NumArray {
    private int[] prefixSum;

    public NumArray(int[] nums) {
        prefixSum = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }
    }
    
    public int sumRange(int left, int right) {
        return prefixSum[right + 1] - prefixSum[left];
    }
}
```

6. Fast and Slow Pointers

Use when:
- You need to detect cycles in a linked list or array.
- You're dealing with problems involving finding the middle element of a linked list.

Example: Detect cycle in a linked list

```java
public class FastSlowPointers {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;
        ListNode slow = head, fast = head.next;
        while (slow != fast) {
            if (fast == null || fast.next == null) return false;
            slow = slow.next;
            fast = fast.next.next;
        }
        return true;
    }
}
```

7. Trie

Use when:
- You're dealing with problems involving strings, especially prefix matching.
- You need to implement autocomplete or spell checker functionalities.

Example: Implement Trie (Prefix Tree)

```java
class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
        }
        node.isEndOfWord = true;
    }
    
    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node != null && node.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        return searchPrefix(prefix) != null;
    }
    
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.children.containsKey(c)) {
                return null;
            }
            node = node.children.get(c);
        }
        return node;
    }
}

class TrieNode {
    Map<Character, TrieNode> children = new HashMap<>();
    boolean isEndOfWord;
}
```

8. Union Find (Disjoint Set)

Use when:
- You need to group elements into disjoint sets.
- You're dealing with problems involving connectivity in graphs.

Example: Number of Connected Components in an Undirected Graph

```java
public class UnionFind {
    private int[] parent;
    private int[] rank;
    private int count;

    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        count = n;
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }

    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
            count--;
        }
    }

    public int getCount() {
        return count;
    }
}
```

9. Iterative DFS

Use when:
- You need to perform a depth-first search but want to avoid stack overflow issues that might occur with recursive DFS.
- You're dealing with problems involving graph or tree traversal where the depth of the structure is unknown or potentially very large.

Example: DFS traversal of a graph

```java
public class IterativeDFS {
    public void dfs(Map<Integer, List<Integer>> graph, int start) {
        Set<Integer> visited = new HashSet<>();
        Stack<Integer> stack = new Stack<>();
        stack.push(start);

        while (!stack.isEmpty()) {
            int node = stack.pop();
            if (!visited.contains(node)) {
                visited.add(node);
                System.out.println(node);  // Process the node

                for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                    if (!visited.contains(neighbor)) {
                        stack.push(neighbor);
                    }
                }
            }
        }
    }
}
```

10. Two Heaps

Use when:
- You need to keep track of the median of a stream of numbers.
- You're dealing with problems that require maintaining two halves of a data set, where you need quick access to the maximum of the smaller half and the minimum of the larger half.

Example: Find Median from Data Stream

```java
class MedianFinder {
    private PriorityQueue<Integer> small;  // max heap
    private PriorityQueue<Integer> large;  // min heap

    public MedianFinder() {
        small = new PriorityQueue<>((a, b) -> b - a);
        large = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        small.offer(num);
        large.offer(small.poll());
        if (small.size() < large.size()) {
            small.offer(large.poll());
        }
    }
    
    public double findMedian() {
        if (small.size() > large.size()) {
            return small.peek();
        } else {
            return (small.peek() + large.peek()) / 2.0;
        }
    }
}
```

Certainly! As an expert software engineer, I'll help you build an intuition for when to use these algorithms and provide Java code samples for each.

11. Subsets (Backtracking)

Use when:
- You need to generate all possible subsets of a set.
- You're dealing with problems that require exploring all combinations of elements.

Example: Generate all subsets of a set

```java
class Subsets {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums, 0);
        return result;
    }

    private void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums, int start) {
        result.add(new ArrayList<>(tempList));
        for (int i = start; i < nums.length; i++) {
            tempList.add(nums[i]);
            backtrack(result, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

12. Combinations (Backtracking)

Use when:
- You need to generate all possible combinations of k elements from a set of n elements.
- You're solving problems that involve selecting a specific number of items from a larger set.

Example: Generate all combinations of k numbers out of 1...n

```java
class Combinations {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), 1, n, k);
        return result;
    }

    private void backtrack(List<List<Integer>> result, List<Integer> tempList, int start, int n, int k) {
        if (tempList.size() == k) {
            result.add(new ArrayList<>(tempList));
            return;
        }
        for (int i = start; i <= n; i++) {
            tempList.add(i);
            backtrack(result, tempList, i + 1, n, k);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

13. Permutations (Backtracking)

Use when:
- You need to generate all possible arrangements of a set of elements.
- You're dealing with problems that require exploring all possible orderings.

Example: Generate all permutations of a set of numbers

```java
class Permutations {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums);
        return result;
    }

    private void backtrack(List<List<Integer>> result, List<Integer> tempList, int[] nums) {
        if (tempList.size() == nums.length) {
            result.add(new ArrayList<>(tempList));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (tempList.contains(nums[i])) continue;
            tempList.add(nums[i]);
            backtrack(result, tempList, nums);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

14. Dijkstra's Algorithm

Use when:
- You need to find the shortest path between nodes in a graph.
- You're dealing with weighted graphs where all weights are non-negative.

Example: Find the shortest path from a source node to all other nodes

```java
class Dijkstra {
    public int[] shortestPath(int[][] graph, int source) {
        int n = graph.length;
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{source, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int node = current[0], distance = current[1];

            if (distance > dist[node]) continue;

            for (int neighbor = 0; neighbor < n; neighbor++) {
                if (graph[node][neighbor] > 0) {
                    int newDist = distance + graph[node][neighbor];
                    if (newDist < dist[neighbor]) {
                        dist[neighbor] = newDist;
                        pq.offer(new int[]{neighbor, newDist});
                    }
                }
            }
        }

        return dist;
    }
}
```

15. Prim's Algorithm

Use when:
- You need to find a minimum spanning tree in a weighted, undirected graph.
- You're dealing with dense graphs.

Example: Find the minimum spanning tree of a graph

```java
class Prims {
    public int minimumSpanningTree(int[][] graph) {
        int n = graph.length;
        boolean[] inMST = new boolean[n];
        int[] key = new int[n];
        Arrays.fill(key, Integer.MAX_VALUE);
        key[0] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.offer(new int[]{0, 0});

        int mstCost = 0;

        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int node = current[0], weight = current[1];

            if (inMST[node]) continue;

            inMST[node] = true;
            mstCost += weight;

            for (int neighbor = 0; neighbor < n; neighbor++) {
                if (!inMST[neighbor] && graph[node][neighbor] > 0 && graph[node][neighbor] < key[neighbor]) {
                    key[neighbor] = graph[node][neighbor];
                    pq.offer(new int[]{neighbor, key[neighbor]});
                }
            }
        }

        return mstCost;
    }
}
```

16. Kruskal's Algorithm

Use when:
- You need to find a minimum spanning tree in a weighted, undirected graph.
- You're dealing with sparse graphs.

Example: Find the minimum spanning tree of a graph

```java
class Kruskals {
    class UnionFind {
        private int[] parent;
        private int[] rank;

        UnionFind(int n) {
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }

        int find(int x) {
            if (parent[x] != x) parent[x] = find(parent[x]);
            return parent[x];
        }

        void union(int x, int y) {
            int px = find(x), py = find(y);
            if (px == py) return;
            if (rank[px] < rank[py]) parent[px] = py;
            else if (rank[px] > rank[py]) parent[py] = px;
            else {
                parent[py] = px;
                rank[px]++;
            }
        }
    }

    public int minimumSpanningTree(int n, int[][] edges) {
        Arrays.sort(edges, (a, b) -> a[2] - b[2]);
        UnionFind uf = new UnionFind(n);
        int mstCost = 0;

        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], weight = edge[2];
            if (uf.find(u) != uf.find(v)) {
                uf.union(u, v);
                mstCost += weight;
            }
        }

        return mstCost;
    }
}
```

17. Topological Sort

Use when:
- You need to order tasks with dependencies.
- You're dealing with directed acyclic graphs (DAGs) and need to find a linear ordering.

Example: Course Schedule II (find order of courses)

```java
class TopologicalSort {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adj = new ArrayList<>(numCourses);
        for (int i = 0; i < numCourses; i++) {
            adj.add(new ArrayList<>());
        }
        for (int[] pre : prerequisites) {
            adj.get(pre[1]).add(pre[0]);
        }

        int[] inDegree = new int[numCourses];
        for (int[] pre : prerequisites) {
            inDegree[pre[0]]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) queue.offer(i);
        }

        int[] order = new int[numCourses];
        int index = 0;
        while (!queue.isEmpty()) {
            int course = queue.poll();
            order[index++] = course;
            for (int next : adj.get(course)) {
                if (--inDegree[next] == 0) {
                    queue.offer(next);
                }
            }
        }

        return index == numCourses ? order : new int[0];
    }
}
```

18. 0-1 Knapsack (DP)

Use when:
- You have a set of items, each with a weight and a value, and you need to determine the most valuable set of items to include in a collection with a weight limit.
- Each item can be included only once (hence "0-1").

Example: 0-1 Knapsack Problem

```java
class Knapsack01 {
    public int knapsack(int[] values, int[] weights, int capacity) {
        int n = values.length;
        int[][] dp = new int[n + 1][capacity + 1];

        for (int i = 1; i <= n; i++) {
            for (int w = 1; w <= capacity; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }

        return dp[n][capacity];
    }
}
```

19. Unbounded Knapsack (DP)

Use when:
- Similar to 0-1 Knapsack, but each item can be used multiple times.
- You're dealing with problems where you can repeatedly use items to maximize value.

Example: Unbounded Knapsack Problem

```java
class UnboundedKnapsack {
    public int unboundedKnapsack(int[] values, int[] weights, int capacity) {
        int[] dp = new int[capacity + 1];

        for (int w = 1; w <= capacity; w++) {
            for (int i = 0; i < values.length; i++) {
                if (weights[i] <= w) {
                    dp[w] = Math.max(dp[w], dp[w - weights[i]] + values[i]);
                }
            }
        }

        return dp[capacity];
    }
}
```

20. Longest Common Subsequence (LCS) (DP)

Use when:
- You need to find the longest subsequence common to two sequences.
- You're dealing with problems involving string matching or comparison.

Example: Longest Common Subsequence

```java
class LCS {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }
}
```

21. Palindromes (DP)

Use when:
- You need to find or count palindromic subsequences or substrings.
- You're dealing with problems involving string manipulations and palindromes.

Example: Longest Palindromic Subsequence

```java
class LongestPalindromicSubsequence {
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        for (int i = n - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[0][n - 1];
    }
}
```

Building Intuition:
- Use Kadane's for maximum subarray problems.
- Use Sliding Window for subarray/substring problems with constraints.
- Use Two Pointers for problems involving pairs or reversing.
- Use Prefix Sums for range sum queries.
- Use Fast and Slow Pointers for cycle detection or finding middle elements.
- Use Trie for string prefix matching and autocomplete.
- Use Union Find for grouping and connectivity problems.
- Use Iterative DFS when recursion might cause stack overflow.
- Use Two Heaps for median maintenance and balancing two halves of data.
- Use Subsets, Combinations, and Permutations for problems requiring exploration of all possibilities.
- Use Dijkstra's for shortest path problems in weighted graphs with non-negative edges.
- Use Prim's or Kruskal's for minimum spanning tree problems, choosing based on graph density.
- Use Topological Sort for ordering tasks with dependencies.
- Use 0-1 Knapsack for optimization problems with indivisible items and a constraint.
- Use Unbounded Knapsack when items can be used multiple times.
- Use LCS for problems involving finding common patterns in sequences.
- Use Palindrome DP for problems involving palindromic properties of strings.
