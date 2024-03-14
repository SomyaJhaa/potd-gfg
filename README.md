## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 14-03-24 

## [Largest subsquare surrounded by X](https://www.geeksforgeeks.org/problems/largest-subsquare-surrounded-by-x0558/1)

## Intuition
Given a square matrix of characters `a[][]` of size `n x n`, we are tasked with finding the largest subsquare containing only the character 'X'. The subsquare must be composed of consecutive 'X's and must be formed by selecting a contiguous set of rows and columns from the matrix.

## Approach

**Dynamic Programming (DP) with 2D Array** : I utilized dynamic programming to solve this problem efficiently. I defined a 2D array `gp[][]` of type `Jora` to store information about the lengths of the subsquares.

**Initialization** : I iterated through each cell `(i, j)` of the matrix. For each cell, if the character is 'X', we initialized a `Jora` object `p` with row and column lengths. If the character is not 'X', we initialized `p` with (0, 0).

**DP Transition** : I updated the lengths of `p.row` and `p.col` based on the adjacent cells. If the character at `(i, j)` is 'X', I checked the left adjacent cell `(i, j - 1)` for row length and the upper adjacent cell `(i - 1, j)` for column length.

**Stored in DP Array** : I stored the `Jora` object `p` in the DP array `gp[i][j]`.

**Founded Maximum Subsquare** : After initializing the DP array, I iterated through the matrix in reverse order. For each cell `(i, j)`, I computed the minimum of `gp[i][j].row` and `gp[i][j].col`. This minimum value represented the potential side length of the largest subsquare that can be formed at cell `(i, j)`.

**Checked Subsquare Validity** : Starting from the potential maximum side length, I iteratively decreased the side length (`s`) and checked if there exists a subsquare of size `s` at cell `(i, j)`. I verified this condition by comparing the row length of the cell `(i, j - s + 1)` and the column length of the cell `(i - s + 1, j)`.

**Updated the Maximum Size** : If a valid subsquare of size `s` is found, I updated the `maxSize` variable to `s`. I continued this process until I have checked all potential subsquare sizes at all cells.

**Returned Maximum Size** : Finally, I returned the maximum subsquare size (`maxSize`) found during the iteration.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( N^2 )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N$ : size of the matrix

- Space complexity : $O( N^2 )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Jora {
    int row;
    int col;
    Jora(int r, int c) {
        row = r;
        col = c;
    }
}

class Solution {
    
    int largestSubsquare(int n, char a[][]) {
        
        // Defining a 2D array to store the lengths of subsquares
        Jora[][] gp = new Jora[n][n];

        // Looping through each cell in the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                
                // Initializing a Jora object with row and column lengths
                Jora p = new Jora(0, 0);
                
                // If the current cell contains 'X', updating the lengths
                if (a[i][j] == 'X') {
                    // Updating row length based on the left adjacent cell
                    p.row = (j - 1 >= 0) ? gp[i][j - 1].row + 1 : 1;
                    // Updating column length based on the upper adjacent cell
                    p.col = (i - 1 >= 0) ? gp[i - 1][j].col + 1 : 1;
                }
                
                // Storing the Jora object in the gp array
                gp[i][j] = p;
            }
        }

        // Initializing a variable to store the maximum subsquare size
        int maxSize = 0;

        // Iterating over the matrix in reverse order to find the largest subsquare
        for (int i = n - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 0; j--) {
                // Getting the minimum of row and column length at the current cell
                int s = Math.min(gp[i][j].row, gp[i][j].col);
                // Iterating from the minimum length to maxSize
                while (s > maxSize) {
                    // Checking if there exists a subsquare of size 's'
                    if (gp[i][j - s + 1].col >= s && gp[i - s + 1][j].row >= s) {
                        // Updating maxSize if a subsquare of larger size is found
                        maxSize = s;
                        break; // Exit the loop once a larger subsquare is found
                    }
                    s--; // Decrementing the size to check smaller subsquares
                }
            }
        }

        // Returning the maximum subsquare size found
        return maxSize;
    }
}
```
