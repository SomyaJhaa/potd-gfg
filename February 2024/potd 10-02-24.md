#  Problem Of The Day Solutions GeeksForGeeks

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 10-02-24 
## [Number of paths in a matrix with k coins](https://www.geeksforgeeks.org/problems/number-of-paths-in-a-matrix-with-k-coins2728/1)

## Intuition

This problem involved finding the number of paths in a 2D matrix from the top-left corner to the bottom-right corner, such that the sum of values along the path is equal to a given target value 'k'. Each cell in the matrix has a value, and I can move only down or right.

To efficiently solve this problem, I employed dynamic programming with memoization. My idea was to store and reuse the results of subproblems to avoid redundant computations.

## Approach

**Initialization :**
- Created a 3D array `gp` to store the intermediate results.
- Initialized all entries of `gp` with -1 to mark them as not computed.

**Recursive Helper Function :**
- Implemented a recursive function `helper` that calculates the number of paths for a given state `(a, b, k)`.
- Base cases :
  - If indices `a` or `b` go out of bounds, or if `k` becomes negative, returned 0.
  - If reaching the top-left corner (a=0, b=0), check if `k` matched the value in the cell. Returned 1 if true, 0 otherwise.
- If the result for the current state is already computed (`gp[a][b][k] != -1`), returned the stored result.
- Recursive case :
  - Calculated the number of paths by moving left (`helper(mat, a - 1, b, k - mat[a][b])`) and up (`helper(mat, a, b - 1, k - mat[a][b])`).
  - Stored the result in `gp[a][b][k]`.

**Main Function (`numberOfPath`) :**
- Initialized `gp` and filled it with intermediate results.
- Called the `helper` function with the input matrix `arr`, dimensions `n` and target sum `k`.
- Returned the final result.

By using dynamic programming and memoization, my approach avoided redundant computations and efficiently calculated the number of paths with the given constraints.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n * n * 101)$ $\equiv$ $O(n^2)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

$n$ : size of the matrix (assuming `n` rows and `n` columns).

- Space complexity : $O(n * n * 101)$ $\equiv$ $O(n^2)$ 
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 

```
//User function Template for Java

class Solution {
    
    // Creating a 3D array to store intermediate results
    static long[][][] gp; 

    // Function to calculate the number of paths
    long numberOfPath(int n, int k, int[][] arr) {
        // Initializing the 3D array with -1
        gp = new long[n][n][101];
        for (int i = 0; i < n; i++){
            for (int j = 0; j < n; j++){
                for (int l = 0; l <= 100; l++){
                    gp[i][j][l] = -1;
                }
            }
        }
 
        // Calling the helper function with the input matrix, dimensions, and k
        return helper(arr, n - 1, n - 1, k);
    }

    // Helper function for recursive calculation
    static long helper(int[][] mat, int a, int b, int k){
        
        // Base case : if indices go out of bounds or k becomes negative
        if (a < 0 || b < 0 || k < 0){
            return 0;
        }
        
        // Base case : if we reach the top-left cell, then checking if k matches the value in the cell
        if (a == 0 && b == 0){
            return (k == mat[a][b] ? 1 : 0);
        }
        
        // If the result for the current state is already computed, then returning it
        if (gp[a][b][k] != -1){
            return gp[a][b][k];
        }
        
        // Recursive case : calculating the number of paths by moving left and up
        gp[a][b][k] = helper(mat, a - 1, b, k - mat[a][b]) + helper(mat, a, b - 1, k - mat[a][b]);
        
        // Returning the computed result for the current state
        return gp[a][b][k];
    }
}
            
```
