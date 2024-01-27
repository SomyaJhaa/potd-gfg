## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 27-01-24 [Problem Link](https://www.geeksforgeeks.org/problems/brackets-in-matrix-chain-multiplication1024/1)
## Brackets in Matrix Chain Multiplication

## Intuition

This problem involves finding the optimal order of multiplying a given set of matrices to minimize the total number of scalar multiplications.


## Approach

**Dynamic Programming Table Initialization :**
   - Initialized a 2D array `gp` to store the minimum cost of multiplying matrices.
   - Set `gp[i][i]` to 0 for all `i`, as a single matrix multiplication has no cost.

**Dynamic Programming Table Filling :**
   - Used a bottom-up approach to fill the `gp` table.
   - For each subsequence length `len` (2 to n-1), iterated through all possible subsequences (i, j) of that length.
   - For each subsequence, found the optimal split point `k` that minimizes the cost of multiplication.
   - Updated the `gp[i][j]` with the minimum cost and store the optimal split point in the `order` array.

**Optimal Order Reconstruction :**
   - After filling the `gp` table, reconstructed the optimal order of matrix multiplication.
   - Used a recursive function `appendOptimalOrder` to traverse the `order` array and build the result string.

**Result :**
   - The result string contained the optimal order of matrix multiplication, including parentheses to represent the optimal split points.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(n^3)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of matrices

- Space complexity : $O(n^2)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 
```
//User function Template for Java

class Solution {
    // Static variable to store the optimal order
    static char[][] order;

    // Main function to find the optimal matrix chain multiplication order
    static String matrixChainOrder(int p[], int n) {
        
        // Initializing the dynamic programming table
        int[][] gp = initializeDPTable(n);
        
        // Initializing the order array to store the optimal split points
        order = new char[n][26]; 

        // Filling the dynamic programming table and order array
        fillDPTable(gp, p, n);
        
        // Reconstructing the optimal order
        reconstructOptimalOrder(gp, order, p, n);

        // Building the result string from the optimal order
        StringBuilder result = new StringBuilder();
        appendOptimalOrder(order, result, 1, n - 1);
        return result.toString();
    }

    // Helper function to initialize the dynamic programming table
    static int[][] initializeDPTable(int n) {
        int[][] gp = new int[n][n];
        for (int i = 1; i < n; i++) {
            gp[i][i] = 0;
        }
        return gp;
    }

    // Helper function to fill the dynamic programming table and order array
    static void fillDPTable(int[][] gp, int[] dimensions, int n) {
        for (int len = 2; len < n; len++) {
            for (int i = 1; i < n - len + 1; i++) {
                int j = i + len - 1;
                gp[i][j] = Integer.MAX_VALUE;

                for (int k = i; k < j; k++) {
                    // Calculating the cost of multiplication
                    int cost = gp[i][k] + gp[k + 1][j] + dimensions[i - 1] * dimensions[k] * dimensions[j];

                    // Updating the dynamic programming table and order array if cost is smaller
                    if (cost < gp[i][j]) {
                        gp[i][j] = cost;
                        order[i][j] = (char) ('A' + k - 1); // Storing the optimal split point
                    }
                }
            }
        }
    }

    // Helper function to reconstruct the optimal order
    static void reconstructOptimalOrder(int[][] gp, char[][] order, int[] dimensions, int n) {
        for (int i = 1; i < n; i++) {
            for (int j = i; j < n; j++) {
                gp[i][j] = Integer.MAX_VALUE;
            }
        }
    }

    // Helper function to append the optimal order to the result string
    static void appendOptimalOrder(char[][] order, StringBuilder result, int i, int j) {
        if (i == j) {
            result.append((char) ('A' + i - 1));
            return;
        }
        result.append('(');
        appendOptimalOrder(order, result, i, order[i][j] - 'A' + 1);
        appendOptimalOrder(order, result, order[i][j] - 'A' + 2, j);
        result.append(')');
    }
}
```

