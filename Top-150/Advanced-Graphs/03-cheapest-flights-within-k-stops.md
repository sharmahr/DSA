[Cheapest Flights within K stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

# Intuition
To find the cheapest price from the source city to the destination city with at most k stops, we can use the Bellman-Ford algorithm. This algorithm allows us to find the shortest path from a source vertex to all other vertices in a weighted graph, even with negative edge weights. In this case, we can modify the algorithm to limit the number of stops.

# Approach
1. Create an array `prices` of size n to store the minimum prices from the source city to each city. Initialize all prices to infinity, except for the source city, which has a price of 0.

2. Iterate k+1 times (to allow for at most k stops):
   - Create a temporary array `temp` to store the updated prices for each iteration.
   - Copy the values from `prices` to `temp`.
   - Loop through each flight:
     - Get the source city `s`, destination city `d`, and the price of the flight.
     - If the price from the source city is infinity, skip this flight as it will not contribute to a valid path.
     - If the price from the source city plus the price of the current flight is less than the current price to the destination city, update the price in `temp`.
   - Update `prices` with the values from `temp`.

3. After the iterations, check if the price to the destination city is not infinity. If it is not, return the price as the cheapest price. Otherwise, return -1 to indicate that there is no valid path within the given number of stops.

# Complexity
- Time complexity: O(k * E)
  - k is the maximum number of stops allowed.
  - E is the number of flights (edges) in the graph.
  - We iterate k+1 times, and in each iteration, we loop through all the flights.

- Space complexity: O(n)
  - n is the number of cities.
  - We use two arrays, `prices` and `temp`, each of size n to store the minimum prices.

# Code
```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        // Implement Bellman-Ford algorithm
        int[] prices = new int[n];
        Arrays.fill(prices, Integer.MAX_VALUE);

        // Price from source to source is always 0
        prices[src] = 0;

        for (int i = 0; i <= k; i++) {
            int[] temp = new int[n];
            temp = Arrays.copyOf(prices, prices.length);

            // Loop through the flights
            for (int j = 0; j < flights.length; j++) {
                int s = flights[j][0]; // Source city
                int d = flights[j][1]; // Destination city
                int price = flights[j][2]; // Price of the flight

                if (prices[s] == Integer.MAX_VALUE) {
                    continue; // Skip if the price from the source city is infinity
                }

                if (prices[s] + price < temp[d]) {
                    temp[d] = prices[s] + price;
                }
            }

            prices = temp;
        }

        if (prices[dst] != Integer.MAX_VALUE) {
            return prices[dst];
        }
        return -1; // No valid path within the given number of stops
    }
}
```