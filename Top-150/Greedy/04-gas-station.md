[Gas Station](https://leetcode.com/problems/gas-station/description/)

# Intuition
The problem of finding the starting gas station for a circular tour can be solved using a greedy approach. The intuition is to keep track of the total gas and total cost as we traverse the stations. If the total cost is greater than the total gas, it means a complete tour is not possible. Otherwise, we can find the starting station by maintaining a running total of the gas minus the cost. Whenever the running total becomes negative, we reset it to zero and consider the next station as a potential starting point.

# Approach
1. Initialize variables:
   - `totalGas` to store the total amount of gas available from all stations.
   - `totalCost` to store the total cost of gas required to travel between all stations.
   - `result` to store the index of the starting gas station for the circular tour.
   - `total` to store the running total of gas minus cost.
2. Iterate through all the gas stations and calculate the total gas and total cost.
3. If the total cost is greater than the total gas, return -1 since a complete tour is not possible.
4. Iterate through all the gas stations again:
   - Update the running total by adding the difference between the gas and cost at the current station.
   - If the running total becomes negative:
     - Reset the running total to zero.
     - Update the result to the index of the next station (i + 1) as a potential starting point.
5. Return the result as the index of the starting gas station for the circular tour.

# Complexity
- Time complexity: O(n), where n is the number of gas stations. We iterate through the stations twice.
- Space complexity: O(1) since we only use a constant amount of extra space for variables.

# Code
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0, totalCost = 0, result = 0, total = 0;

        for(int i=0;i<gas.length;i++){
            totalGas += gas[i];
            totalCost += cost[i];
        }

        if(totalCost > totalGas) return -1; // answer is not possible

        for(int i=0;i<gas.length;i++){
            total += gas[i] - cost[i];
            if(total < 0){
                total = 0;
                result = i + 1;
            }
        }

        return result;
    }
}
```