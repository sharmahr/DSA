

# Intuition
To determine if a person can attend all the meetings without any overlap, we can sort the intervals based on their start times. If there is any overlap between consecutive intervals after sorting, it means the person cannot attend all the meetings. The intuition is that by sorting the intervals based on start times, we can easily check for overlaps by comparing the end time of one interval with the start time of the next interval.

# Approach
1. Sort the intervals based on their start times in ascending order. We can use a custom comparator to compare the start times of two intervals.
2. Iterate through the sorted intervals from index 0 to `intervals.size() - 2` (since we will compare each interval with the next one):
   - Get the current interval.
   - Compare the end time of the current interval with the start time of the next interval.
   - If the end time of the current interval is greater than the start time of the next interval, it means there is an overlap, so return `false`.
3. If the loop completes without finding any overlaps, return `true` since the person can attend all the meetings.

# Complexity
- Time complexity: O(n log n), where n is the number of intervals. Sorting the intervals takes O(n log n) time, and iterating through the sorted intervals takes O(n) time.
- Space complexity: O(1) since we only use a constant amount of extra space for the custom comparator and temporary variables.

# Code
```java
/**
 * Definition of Interval:
 * public class Interval {
 *     public int start, end;
 *     public Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

class Solution {
    public boolean canAttendMeetings(List<Interval> intervals) {
        // Sort the intervals based on the start time
        Collections.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval first, Interval second) {
                return Integer.compare(first.start, second.start);
            }
        });

        for (int i = 0; i < intervals.size() - 1; i++) {
            Interval interval = intervals.get(i);
            if (interval.end > intervals.get(i + 1).start) {
                return false;
            }
        }

        return true;
    }
}
```