## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 08-04-24

## [Optimal Strategy For A Game](https://www.geeksforgeeks.org/problems/optimal-strategy-for-a-game-1587115620/1)

## Intuition
The task is to maximize the amount of money obtained by selecting coins optimally from the given array. This problem can be efficiently solved using dynamic programming.

## Approach

**Initialization** : 
- Initialize an array `a` with the given coin values.
- Initialize a memoization table `gp` to store computed values.

**Recursive Function** (`helper`) :
- Defined a function to recursively compute the maximum amount.
- Base case : Returned 0 if left pointer exceeds right pointer or if the value is already computed.
- Recursive Step : Computed the maximum amount by selecting coins optimally.

**Main Function** (`countMaximum`) :
- Initialized variables and called the recursive function with initial parameters.
- Returned the computed result.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(c^2)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$c$ : number of coins
- Space complexity : $O(c^2)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class solve {
    
    static int[] a;
    static long gp[][];
    
    //Function to find the maximum possible amount of money we can win
    static long countMaximum(int n, int[] arr) {
       
        // Your code here
     
        // Assigning the array and initializing the memoization table
        a = arr;
        gp = new long[n][n];
        
        // Filling the memoization table with -1 to indicate not yet computed values
        for (long[] row : gp) {
            Arrays.fill(row, -1);
        }
        
        // Calling the recursive helper function to find the maximum amount
        return helper(0, n - 1);
    }

    // Recursive helper function to find the maximum amount by choosing coins optimally
    static long helper(int l, int r) {
        // Base case: when left pointer exceeds the right pointer, returning 0
        if (l > r){
            return 0;
        }
        
        // If the value for the current range [l, r] is already computed, returning it
        if (gp[l][r] != -1){
            return gp[l][r];
        } 
        
        // Calculating the maximum amount by choosing coins optimally
        gp[l][r] = Math.max(a[l] + Math.min(helper(l + 2, r), helper(l + 1, r - 1)),
                            a[r] + Math.min(helper(l, r - 2), helper(l + 1, r - 1)));
        
        return gp[l][r];
    }

}
```
