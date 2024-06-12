# Binary Search
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [Binary Search](https://leetcode.com/problems/binary-search/description/) | The intuition is to repeatedly divide the search interval in half by comparing the middle element with the target value. If the middle element is equal to the target, we have found the solution. If the target is greater than the middle element, we search in the right half of the interval. Otherwise, we search in the left half of the interval. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/1-binary-search.md) |
| [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/description/) | The intuition is to treat the 2D matrix as a single sorted array and perform binary search on it. By flattening the matrix into a 1D array, we can leverage the existing binary search algorithm for sorted arrays or you can perform binary search without flattening the matrix just use the correct values of right and left. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/2-search-a-2d-matrix.md) |
| [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/description/) | We can start with a minimum possible speed of 1 banana per hour and a maximum possible speed equal to the maximum pile size. Then, we can perform a binary search on the range of possible speeds and check if the current speed allows Koko to eat all the bananas within the given hour constraint. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/3-koko-eating-bananas.md) |
| [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/) | Idea is to find the pivot point where the value transitions from a larger value to a smaller value. This pivot point is the minimum value in the rotated sorted array. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/4-find-minimum-in-rotated-sorted-array.md) |
| [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/) | Identify which half of the array is sorted and determine if the target element lies within that sorted half. By comparing the middle element with the target and the endpoints of the current search range, we can recursively narrow down the search space until the target is found or the search range is exhausted. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/5-search-in-rotated-sorted-array.md) |
| [Time Based Key Value Store](https://leetcode.com/problems/time-based-key-value-store/description/) | The intuition is to use a hash map to store the key-value pairs, where each key maps to a list of values along with their corresponding timestamps. To retrieve the value for a given key and timestamp, we can perform a binary search on the list of values to find the value with the highest timestamp less than or equal to the given timestamp. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/6-time-based-key-value-store.md) |
| [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/) | Perform a binary search on the smaller array to find the partition point that divides both arrays into left and right halves such that the elements in the left half are smaller than or equal to the elements in the right half. Once we find the correct partition, we can determine the median based on the maximum element in the left half and the minimum element in the right half. | [Solution](https://github.com/sharmahr/DSA/blob/main/Top-150/Binary-Search/7-median-of-two-sorted-arrays.md) |