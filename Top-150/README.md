# Arrays And Hashing
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/) | Use the input array itself as a hash table to keep track of the elements we have encountered so far. By negating the value at the index corresponding to each element, we can mark it as visited. If we encounter a negative value at an index, it means we have already visited that element before, indicating a duplicate. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/1-contains-duplicate.md) |
| [Valid Anagram](https://leetcode.com/problems/valid-anagram/description/) | Count the frequency of each character in both strings and compare them or sort the strings and compare. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/2-valid-anagram.md) |
| [Two Sum](https://leetcode.com/problems/two-sum/) | Use a hashmap to store the elements of the array along with their indices | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/3-two-sum.md) |
| [Group Anagrams](https://leetcode.com/problems/group-anagrams/) | Use a hashmap where the key is a sorted version of each word, and the value is a list of words that are anagrams of each other | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/4-group-anagrams.md) |
| [Top K frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | use a hash map to count the frequency of each element and then use a priority queue (min-heap) to keep track of the top k frequent elements. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/5-top-k-frequent-elements.md) |
| [Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode) | Use a delimiter to separate the individual strings and include the length of each string before the delimiter to facilitate the decoding process. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/6-encode-decode-strings.md) |
| [Product of Array and Sef](https://leetcode.com/problems/product-of-array-except-self/description/) | Calculate the product of all the elements to the left of each index and the product of all the elements to the right of each index, and then multiply these two values to get the desired result. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/7-product-of-array-except-self.md) |
| [Valid Sudodu](https://leetcode.com/problems/valid-sudoku/description/) | Check the validity of each row, column, and 3x3 block separately. We can use a set to keep track of the numbers encountered in each row, column, and block. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/8-valid-sudoku.md) |
| [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/) | Use a hash set to store all the numbers in the array and then iterate through the set to find the longest consecutive sequence | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Arrays-And-Hashing/9-longest-consecutive-sequence.md) |



# Two Pointers
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [Valid Palidrome](https://leetcode.com/problems/valid-palindrome/description/) | Use two pointers, one starting from the beginning and the other from the end of the string, and move them inwards while skipping non-alphanumeric characters. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Two-Pointers/1-valid-palindrome.md) |
| [Two Sum Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | Use the two-pointer approach, where we start with two pointers, one at the beginning and one at the end of the array, and move them based on the sum of the elements they point to. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Two-Pointers/2-two-sum-input-array-is-sorted.md) |
| [3Sum](https://leetcode.com/problems/3sum/description/) | Extend the two-pointer approach used in the two-sum problem to solve this problem. We can first sort the array, and then fix one element at a time. For each fixed element, we can use the two-pointer technique to find the other two elements that sum up to the negative of the fixed element. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Two-Pointers/3-3sum.md) |
| [Container with Most Water](https://leetcode.com/problems/container-with-most-water/description/) | Use two pointers, one at the beginning and one at the end of the array, and move them inwards to find the maximum area. The area is determined by the smaller of the two heights and the distance between the two lines. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Two-Pointers/4-container-with-most-water.md) |
| [Rainwater Trapping](https://leetcode.com/problems/trapping-rain-water/description/) | Use two pointers, one starting from the left and the other from the right, and keep track of the maximum height seen from both sides. The amount of water trapped at any point is determined by the minimum of the maximum heights on both sides and the current height. | [Solution](https://github.com/sharmahr/DSA/Neetcode-150/Two-Pointers/5-trapping-rain-water.md) |


# Sliding Window
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |


### Binary Search
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |

### Linked List
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |

### Trees
| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |
| Row 3, Cell 1 | Row 3, Cell 2 | Row 3, Cell 3 |