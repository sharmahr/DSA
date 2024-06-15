[Insert Interval](https://leetcode.com/problems/insert-interval/)

# Intuition
To insert a new interval into a list of non-overlapping intervals, we can iterate through the existing intervals and merge the new interval with any overlapping intervals. The intuition is to find the appropriate position to insert the new interval and merge it with any overlapping intervals.

# Approach
1. Create an ArrayList `result` to store the resulting intervals.
2. Iterate through the existing intervals:
   - If the current interval's end time is less than the start time of the new interval, add the current interval to the `result` list.
   - If the current interval's start time is greater than the end time of the new interval, add the new interval to the `result` list and update the new interval to the current interval.
   - If there is an overlap between the current interval and the new interval, merge them by updating the start time of the new interval to the minimum of the two start times and the end time of the new interval to the maximum of the two end times.
3. Add the last merged interval (if any) to the `result` list.
4. Convert the `result` list to a 2D array and return it.

# Complexity
- Time complexity: O(n), where n is the number of intervals. We iterate through the intervals once.
- Space complexity: O(n) to store the resulting intervals in the `result` list.

# Code
```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> result = new ArrayList<>();

        for (int[] interval : intervals) {
            if (interval[1] < newInterval[0]) {
                result.add(interval);
            } else if (interval[0] > newInterval[1]) {
                result.add(newInterval);
                newInterval = interval;
            } else {
                newInterval[0] = Math.min(newInterval[0], interval[0]);
                newInterval[1] = Math.max(newInterval[1], interval[1]);
            }
        }

        result.add(newInterval);

        return result.toArray(new int[result.size()][]);
    }
}
```