## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 23-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/buy-and-sell-a-share-at-most-twice/1)
## Buy and Sell a Share at most twice

## Intuition
This problem involves finding the maximum profit that can be obtained from at most two transactions in a given set of stock prices. The goal is to identify the best times to buy and sell stocks to maximize profit.

## Approach

**Dynamic Programming :**
   - I used a dynamic programming approach with a 3D array (`gp`) to store intermediate results. The array is defined as `gp[i][j][k]`, where `i` represents the day, `j` represents whether a stock is held (0 for not held, 1 for held), and `k` represents the number of transactions completed.

**Base Cases :**
   - Initialized the last day values in the `gp` array based on the base case where no transactions are allowed.

**Dynamic Programming Iteration :**
   - Iterated backward through the array of stock prices, considering different states:
     - Calculated the maximum profit when not holding a stock (`gp[i][0][j]`).
     - Calculated the maximum profit when holding a stock (`gp[i][1][j]`), considering the possibility of a stock being bought on the current day.
     - Updated the `gp` array based on these calculations.

**Final Result :**
   - The maximum profit considering at most two transactions and not holding a stock on the first day is stored in `gp[0][0][2]`.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n)$ 
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of days or the length of the input stock prices array

- Space complexity : $O((n+1) \cdot 2 \cdot 3)$ ${\cong}$ $O(n)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
   
## Code 

```
//User function Template for Java

class Solution {
    
    // 3D array to store intermediate results during dynamic programming
    static int[][][] gp;

    // Function to calculate the maximum profit
    public static int maxProfit(int n, int[] price) {
        
        // Initializing the 3D array for dynamic programming
        gp = new int[n + 1][2][3];

        // Base case : no transactions allowed
        for (int k = 0; k < 3; k++) {
            gp[n][0][k] = 0;
            gp[n][1][k] = 0;
        }

        // Bottom-up dynamic programming
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < 3; j++) {
                // Calculating the maximum profit when not holding a stock
                gp[i][0][j] = Math.max(-price[i] + gp[i + 1][1][j], gp[i + 1][0][j]);

                // Calculating the maximum profit when holding a stock
                if (j > 0) {
                    gp[i][1][j] = Math.max(price[i] + gp[i + 1][0][j - 1], gp[i + 1][1][j]);
                }
            }
        }

        // Returning the maximum profit considering no stock held on the first day
        return gp[0][0][2];
    }
}
```
