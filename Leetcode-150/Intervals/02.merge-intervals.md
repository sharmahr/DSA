[Merge Intervals](https://leetcode.com/problems/merge-intervals/)

# Intuition
To merge overlapping intervals, we can sort the intervals based on their start times and then iterate through the sorted intervals. If the current interval's start time is less than or equal to the end time of the previous interval, we merge them by updating the end time of the previous interval to the maximum of the two end times. Otherwise, we add the previous interval to the result list and update the previous interval to the current interval.

# Approach
1. Sort the intervals based on their start times using a custom comparator that compares the start times of two intervals.
2. Create an ArrayList `merged` to store the merged intervals.
3. Initialize the `prev` interval as the first interval in the sorted array.
4. Iterate through the sorted intervals starting from index 1:
   - If the current interval's start time is less than or equal to the end time of the `prev` interval, merge them by updating the end time of `prev` to the maximum of the two end times.
   - Otherwise, add the `prev` interval to the `merged` list and update `prev` to the current interval.
5. Add the last `prev` interval to the `merged` list.
6. Convert the `merged` list to a 2D array and return it.

# Complexity
- Time complexity: O(n log n), where n is the number of intervals. Sorting the intervals takes O(n log n) time, and iterating through the sorted intervals takes O(n) time.
- Space complexity: O(n) to store the merged intervals in the `merged` list.

# Code
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        List<int[]> merged = new ArrayList<>();
        int[] prev = intervals[0];

        for (int i = 1; i < intervals.length; i++) {
            int[] interval = intervals[i];
            if (interval[0] <= prev[1]) { // compare the start of the current interval with the end of the prev
                prev[1] = Math.max(prev[1], interval[1]);
            } else {
                merged.add(prev);
                prev = interval;
            }
        }

        merged.add(prev); //add the last value to the merged list

        return merged.toArray(new int[merged.size()][]);
    }
}
```