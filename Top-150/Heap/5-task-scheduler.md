[Task Scheduler](https://leetcode.com/problems/task-scheduler/)

# Intuition
To solve this problem, we can use a greedy approach. The idea is to schedule the tasks with the highest frequency first and distribute them evenly with cooling intervals in between. We can determine the minimum number of intervals required based on the maximum frequency of the tasks and the number of tasks with the maximum frequency.

# Approach
1. Create an array `freq` of size 26 to store the frequency of each task.
2. Iterate through the `tasks` array and count the frequency of each task by incrementing the corresponding element in the `freq` array.
3. Sort the `freq` array in descending order to easily find the maximum frequency and the number of tasks with the maximum frequency.
4. Find the maximum frequency `maxFreq` by accessing the last element of the sorted `freq` array.
5. Count the number of tasks with the maximum frequency `maxCount` by iterating from the second-to-last element of the `freq` array towards the beginning until an element not equal to `maxFreq` is found.
6. Calculate the minimum number of intervals required using the formula `(maxFreq - 1) * (n + 1) + maxCount`. This formula distributes the tasks with the maximum frequency evenly with cooling intervals in between.
7. Return the maximum of `intervals` and the total number of tasks (`tasks.length`) to handle the case where the calculated `intervals` is smaller than the total number of tasks.

# Complexity
- Time complexity: $O(n \log n)$
The time complexity is dominated by the sorting step, which takes $O(n \log n)$ time, where $n$ is the length of the `tasks` array. The other operations, such as counting frequencies and calculating intervals, take $O(n)$ time.

* Space complexity: $O(1)$
The space complexity is $O(1)$ because we use a fixed-size array `freq` of size 26 to store the frequencies of the tasks, regardless of the input size. The space required for sorting and other variables is constant.

# Code
```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        // Create an array to store the frequency of each task
        int[] freq = new int[26];
        
        // Count the frequency of each task
        for (char task : tasks) {
            freq[task - 'A']++;
        }
        
        // Sort the frequency array in descending order
        Arrays.sort(freq);
        
        // Find the maximum frequency
        int maxFreq = freq[25];
        
        // Count the number of tasks with the maximum frequency
        int maxCount = 1;
        for (int i = 24; i >= 0 && freq[i] == maxFreq; i--) {
            maxCount++;
        }
        
        // Calculate the minimum number of intervals required
        int intervals = (maxFreq - 1) * (n + 1) + maxCount;
        
        // Return the maximum of intervals and the total number of tasks
        return Math.max(intervals, tasks.length);
    }
}
```