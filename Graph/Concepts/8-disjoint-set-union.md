[Disjoint Set Union](https://www.geeksforgeeks.org/problems/disjoint-set-union-find/1)

# Intuition
The problem requires implementing a disjoint set data structure, also known as a union-find data structure. The intuition behind solving this problem is to use an array to represent the sets and perform two main operations: find and union. The find operation determines the parent or representative of a set, while the union operation merges two sets together.

Note to remember: Path compression is used in the find operation to optimize the time complexity by flattening the tree structure.

# Approach
1. Implement the `find` function:
   - Take an array `A` and an element `X` as input.
   - Check if `A[X]` is not equal to `X` (i.e., `X` is not the parent of itself).
     - If true, recursively call `find(A, A[X])` to find the parent of `X` and update `A[X]` with the parent (path compression).
   - Return `A[X]`, which represents the parent or representative of the set.

2. Implement the `unionSet` function:
   - Take an array `A` and two elements `X` and `Z` as input.
   - Find the parents of `X` and `Z` using the `find` function and store them in `parentX` and `parentZ`, respectively.
   - Update `A[parentX]` to `parentZ` to merge the sets containing `X` and `Z`.

# Complexity
- Time complexity:
  - The `find` operation has a time complexity of $O(\alpha(n))$, where $\alpha$ is the inverse Ackermann function. In practice, it is nearly constant time.
  - The `unionSet` operation also has a time complexity of $O(\alpha(n))$ due to the `find` operations.
* Space complexity:
  - The space complexity is $O(n)$, where $n$ is the size of the array `A`.

# Code
```java
class GfG {
    int find(int A[], int X) {
        // Find the parent of X with path compression
        if (A[X] != X) {
            A[X] = find(A, A[X]);
        }
        return A[X];
    }

    void unionSet(int A[], int X, int Z) {
        // Find the parents of X and Z
        int parentX = find(A, X);
        int parentZ = find(A, Z);

        // Make the parent of Z the parent of X
        A[parentX] = parentZ;
    }
}
```