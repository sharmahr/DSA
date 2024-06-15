[Non Overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

# Intuition
To minimize the number of intervals to be removed to make the remaining intervals non-overlapping, we can use a greedy approach. The intuition is to sort the intervals based on their end times and then iterate through the sorted intervals. If the current interval overlaps with the previous interval, we remove the current interval. Otherwise, we keep the current interval and update the end time of the previous interval to the end time of the current interval.

# Approach
1. If the intervals array is empty, return 0 since no intervals need to be removed.
2. Sort the intervals based on their end times using a custom comparator that compares the end times of two intervals.
3. Initialize a variable `count` to keep track of the number of intervals to be removed.
4. Initialize a variable `lastEnd` to store the end time of the previous non-overlapping interval. Initially, set it to the end time of the first interval.
5. Iterate through the sorted intervals starting from the second interval:
   - If the start time of the current interval is less than `lastEnd`, it means there is an overlap. Increment `count` to indicate that the current interval needs to be removed.
   - Otherwise, there is no overlap. Update `lastEnd` to the end time of the current interval.
6. Return the value of `count`, which represents the minimum number of intervals to be removed.

# Complexity
- Time complexity: O(n log n), where n is the number of intervals. Sorting the intervals takes O(n log n) time, and iterating through the sorted intervals takes O(n) time.
- Space complexity: O(1) since we only use a constant amount of extra space for variables.

# Code
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if (intervals.length == 0) return 0;

        // Sort intervals based on end time
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));

        int count = 0;
        int lastEnd = intervals[0][1];

        // Start from the second interval and check for overlap
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] < lastEnd) {
                // Overlapping interval, increment count
                count++;
            } else {
                // No overlap, update lastEnd to the end of the current interval
                lastEnd = intervals[i][1];
            }
        }

        return count;
    }
}
```