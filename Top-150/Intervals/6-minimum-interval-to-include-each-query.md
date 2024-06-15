[Minimum Interval to include each Query](https://leetcode.com/problems/minimum-interval-to-include-each-query/)

# Intuition
To find the size of the smallest interval that contains each query value, we can use a min-heap to keep track of the intervals sorted by their size. The intuition is to sort both the intervals and queries, then iterate through the queries. For each query, we add all the intervals whose start time is less than or equal to the query value to the min-heap. We remove the intervals whose end time is less than the query value from the min-heap. The top of the min-heap will be the smallest interval that contains the query value.

# Approach
1. Initialize an array `result` to store the result for each query, filled with -1 initially.
2. Sort the intervals array based on the start time.
3. Create a 2D array `sortedQueries` to store the queries along with their original indices.
4. Sort the `sortedQueries` array based on the query values.
5. Create a min-heap `minHeap` to store the intervals sorted by their size (end time - start time + 1).
6. Initialize a variable `intervalIndex` to keep track of the current interval.
7. Iterate through each query in `sortedQueries`:
   - Get the query value and its original index.
   - While `intervalIndex` is less than the length of `intervals` and the start time of the current interval is less than or equal to the query value, add the interval to the min-heap and increment `intervalIndex`.
   - While the min-heap is not empty and the end time of the top interval in the min-heap is less than the query value, remove the top interval from the min-heap.
   - If the min-heap is not empty, the top interval in the min-heap is the smallest interval that contains the query value. Update the result array at the original index with the size of the smallest interval.
8. Return the `result` array.

# Complexity
- Time complexity: O((n + q) log(n + q)), where n is the number of intervals and q is the number of queries. Sorting the intervals and queries takes O((n + q) log(n + q)) time. Iterating through the queries and performing operations on the min-heap takes O(q log n) time in the worst case.
- Space complexity: O(n + q) to store the sorted intervals, sorted queries, and the min-heap.

# Code
```java
class Solution {
    public int[] minInterval(int[][] intervals, int[] queries) {
        int[] result = new int[queries.length];
        Arrays.fill(result, -1);
        
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        int[][] sortedQueries = new int[queries.length][2];
        for (int i = 0; i < queries.length; i++) {
            sortedQueries[i][0] = queries[i];
            sortedQueries[i][1] = i;
        }
        Arrays.sort(sortedQueries, (a, b) -> Integer.compare(a[0], b[0]));
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> Integer.compare(a[1] - a[0], b[1] - b[0]));
        int intervalIndex = 0;
        
        for (int[] query : sortedQueries) {
            int queryValue = query[0];
            int originalIndex = query[1];
            
            while (intervalIndex < intervals.length && intervals[intervalIndex][0] <= queryValue) {
                minHeap.offer(new int[] {intervals[intervalIndex][0], intervals[intervalIndex][1]});
                intervalIndex++;
            }
            
            while (!minHeap.isEmpty() && minHeap.peek()[1] < queryValue) {
                minHeap.poll();
            }
            
            if (!minHeap.isEmpty()) {
                int[] smallestInterval = minHeap.peek();
                result[originalIndex] = smallestInterval[1] - smallestInterval[0] + 1;
            }
        }
        
        return result;
    }
}
```