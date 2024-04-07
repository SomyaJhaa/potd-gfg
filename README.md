## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 07-04-24

## [Maximize dot product](https://www.geeksforgeeks.org/problems/maximize-dot-product2649/1)

## Intuition
Given two arrays `a` and `b`, I aim to maximize the dot product by inserting zeros in array `b`, while preserving the order of elements from both arrays.

## Approach

I solve this using Dynamic Programming :

- I initialized a 2D array `dp` to store maximum dot products.
- Iterated through arrays `a` and `b`.
- Calculated dot products at each index pair and update `dp` accordingly.
- Returned `dp[m][n]`, representing the maximum dot product.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n*m)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : given

$m$ : given
- Space complexity : $O(n*m)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution{
    
	public int maxDotProduct(int n, int m, int a[], int b[]) { 
		// Your code goes here
	
		 // Initializing a 2D array to store the maximum dot product
                 int[][] gp = new int[m + 1][n + 1];
        
                 // Initializing the array with zeros
                 for (int[] row : gp) {
                     Arrays.fill(row, 0);
                 }
        
                 // Dynamic programming approach to calculate the maximum dot product
                 for (int i = 1; i <= m; i++) {
                     for (int j = i; j <= n; j++) {
                     // Calculating the current dot product and update the cell
                     gp[i][j] = Math.max(gp[i - 1][j - 1] + a[j - 1] * b[i - 1], gp[i][j - 1]);
                     }
                 }
        
                // Returning the maximum dot product
                return gp[m][n];
	} 
}
```
