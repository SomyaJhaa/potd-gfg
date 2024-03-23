## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 23-03-24 

## [Fibonacci series up to Nth term](https://www.geeksforgeeks.org/problems/fibonacci-series-up-to-nth-term/1)

## Intuition
- The Fibonacci series starts with 0 and 1, where each subsequent number is the sum of the two preceding ones.
- To handle large Fibonacci numbers and prevent overflow, each Fibonacci number is computed modulo `1_000_000_007`.

## Approach

**Initialize Variables :** 
- Create a static integer array `a[]` to store the Fibonacci series elements.
- Allocate memory for `n + 1` elements in the array to accommodate the Fibonacci series up to the `n`th term.
  
**Base Cases :**
- The first two terms of the Fibonacci series are `0` and `1`, which are stored at indices `0` and `1` of the array `a[]`.

**Generate Fibonacci Series :**
- Starting from index `2`, iterate through the array and compute each term by adding the previous two terms.
- To prevent overflow, compute each Fibonacci number modulo `1_000_000_007`.

**Return Result :**
- After generating the Fibonacci series, return the array `a[]` containing the Fibonacci series with each number modulo `1_000_000_007`.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : given
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {

    static int a[]; // Static array to store Fibonacci series elements
    
    // Method to generate Fibonacci series up to the nth term
    int[] Series(int n) {
        
        // Initializing the array to store Fibonacci series
        a = new int[1 + n]; // Allocate memory for 'n' + 1 elements
        
        // Base cases for Fibonacci series
        a[0] = 0; // First term is 0
        a[1] = 1; // Second term is 1
        
        // Generating Fibonacci series
        for (int i = 2; i < a.length; i++) {
            // Computing each term by adding the previous two terms
            // Taking modulus as said
            a[i] = ( a[i - 1] + a[i - 2] ) % 1_000_000_007;
        }
        
        return a; // Returning the array containing Fibonacci series
    }
}
```
