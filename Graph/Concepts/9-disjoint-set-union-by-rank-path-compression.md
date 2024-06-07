[Disjoint Set Union](https://www.geeksforgeeks.org/problems/disjoint-set-union-find/1)

# Intuition
The problem requires implementing a disjoint set data structure with union by rank optimization. The intuition behind solving this problem is to use an array to represent the sets and perform two main operations: find and union. The find operation determines the parent or representative of a set, while the union operation merges two sets together based on their ranks.

Note to remember: Path compression is used in the find operation to optimize the time complexity by flattening the tree structure, and union by rank is used to keep the tree balanced and minimize the depth.

# Approach
1. Implement the `find` function:
   - Take an array `A` and an element `X` as input.
   - Check if `A[X]` is negative (i.e., `X` is the parent of itself and its rank is stored as a negative value).
     - If true, return `X` as it is the parent.
   - Otherwise, recursively call `find(A, A[X])` to find the parent of `X` and update `A[X]` with the parent (path compression).
   - Return `A[X]`, which represents the parent or representative of the set.

2. Implement the `unionSet` function:
   - Take an array `A` and two elements `X` and `Z` as input.
   - Find the parents of `X` and `Z` using the `find` function and store them in `parentX` and `parentZ`, respectively.
   - Check if `parentX` and `parentZ` are different (i.e., `X` and `Z` belong to different sets).
     - If true, perform union by rank:
       - Compare the ranks of `parentX` and `parentZ` (stored as negative values in `A[parentX]` and `A[parentZ]`).
       - If `A[parentX]` is smaller (i.e., `parentX` has a higher rank), update `A[parentX]` by adding `A[parentZ]` to it and make `parentZ` point to `parentX`.
       - Otherwise, update `A[parentZ]` by adding `A[parentX]` to it and make `parentX` point to `parentZ`.

# Complexity
- Time complexity:
  - The `find` operation has a time complexity of $O(\alpha(n))$, where $\alpha$ is the inverse Ackermann function. In practice, it is nearly constant time.
  - The `unionSet` operation also has a time complexity of $O(\alpha(n))$ due to the `find` operations and the union by rank optimization.
* Space complexity:
  - The space complexity is $O(n)$, where $n$ is the size of the array `A`.

# Code
```java
class GfG {
    int find(int A[], int X) {
        // Find the parent of X with path compression
        if (A[X] < 0) {
            return X;
        }
        return A[X] = find(A, A[X]);
    }

    void unionSet(int A[], int X, int Z) {
        // Find the parents of X and Z
        int parentX = find(A, X);
        int parentZ = find(A, Z);

        // Union by rank
        if (parentX != parentZ) {
            if (A[parentX] < A[parentZ]) {
                A[parentX] += A[parentZ];
                A[parentZ] = parentX;
            } else {
                A[parentZ] += A[parentX];
                A[parentX] = parentZ;
            }
        }
    }
}
```