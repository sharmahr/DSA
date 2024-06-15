[Detect Squares](https://leetcode.com/problems/detect-squares/description/)

# Intuition
The problem is to design a data structure that can add points to a 2D grid and count the number of squares that can be formed using the added points. The intuition is to store the coordinates of the added points in a list and use a hash map to keep track of the count of each unique point. When counting the squares, we iterate over the stored coordinates and check for valid square formations.

# Approach
1. Initialize an empty list `coordinates` to store the coordinates of the added points.
2. Initialize an empty hash map `counts` to store the count of each unique point.
3. Implement the `add` method:
   - Add the given point to the `coordinates` list.
   - Create a key by concatenating the x and y coordinates of the point using a delimiter (e.g., "@").
   - Update the count of the point in the `counts` hash map by incrementing its value or setting it to 1 if it doesn't exist.
4. Implement the `count` method:
   - Initialize a variable `sum` to store the total count of squares.
   - Iterate over each coordinate in the `coordinates` list:
     - Check if the current coordinate forms a valid square with the given point.
       - If the x-coordinates or y-coordinates are the same, or the absolute difference between the x-coordinates is not equal to the absolute difference between the y-coordinates, skip the current coordinate.
     - Calculate the count of squares formed by the current coordinate and the given point using the counts stored in the `counts` hash map.
       - Multiply the count of points with the same x-coordinate as the current coordinate and the same y-coordinate as the given point, with the count of points with the same x-coordinate as the given point and the same y-coordinate as the current coordinate.
     - Add the count of squares to the `sum` variable.
   - Return the total count of squares.

# Complexity
- Time complexity:
  - `add` method: $O(1)$
    - Adding a point to the `coordinates` list and updating the count in the `counts` hash map takes constant time.
  - `count` method: $O(n)$, where $n$ is the number of added points.
    - We iterate over each coordinate in the `coordinates` list once.
- Space complexity: $O(n)$, where $n$ is the number of added points.
  - The `coordinates` list and `counts` hash map store the coordinates and counts of the added points, respectively.

# Code
```java
class DetectSquares {
    List<int[]> coordinates;
    Map<String, Integer> counts;
    
    public DetectSquares() {
        coordinates = new ArrayList<>();
        counts = new HashMap<>();
    }
    
    public void add(int[] point) {
        coordinates.add(point);
        String key = point[0] + "@" + point[1];
        counts.put(key, counts.getOrDefault(key, 0) + 1);
    }
    
    public int count(int[] point) {
        int sum = 0, px = point[0], py = point[1];
        for (int[] coordinate : coordinates) {
            int x = coordinate[0], y = coordinate[1];
            if (px == x || py == y || (Math.abs(px - x) != Math.abs(py - y)))
                continue;
            sum += counts.getOrDefault(x + "@" + py, 0) * counts.getOrDefault(px + "@" + y, 0);
        }
        
        return sum;
    }
}
```