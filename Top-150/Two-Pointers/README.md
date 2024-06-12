# Two Pointers
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [Valid Palidrome](https://leetcode.com/problems/valid-palindrome/description/) | Use two pointers, one starting from the beginning and the other from the end of the string, and move them inwards while skipping non-alphanumeric characters. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Two-Pointers/1-valid-palindrome.md) |
| [Two Sum Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | Use the two-pointer approach, where we start with two pointers, one at the beginning and one at the end of the array, and move them based on the sum of the elements they point to. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Two-Pointers/2-two-sum-input-array-is-sorted.md) |
| [3Sum](https://leetcode.com/problems/3sum/description/) | Extend the two-pointer approach used in the two-sum problem to solve this problem. We can first sort the array, and then fix one element at a time. For each fixed element, we can use the two-pointer technique to find the other two elements that sum up to the negative of the fixed element. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Two-Pointers/3-3sum.md) |
| [Container with Most Water](https://leetcode.com/problems/container-with-most-water/description/) | Use two pointers, one at the beginning and one at the end of the array, and move them inwards to find the maximum area. The area is determined by the smaller of the two heights and the distance between the two lines. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Two-Pointers/4-container-with-most-water.md) |
| [Rainwater Trapping](https://leetcode.com/problems/trapping-rain-water/description/) | Use two pointers, one starting from the left and the other from the right, and keep track of the maximum height seen from both sides. The amount of water trapped at any point is determined by the minimum of the maximum heights on both sides and the current height. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Two-Pointers/5-trapping-rain-water.md) |