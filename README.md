## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 12-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/recursive-sequence1611/1)
## Recursive sequence

## Intuition
My code aimed to calculate a sequence based on the given logic. It used modular arithmetic to prevent integer overflow while performing calculations. The sequence involved iteratively multiplying consecutive integers starting from 1 and accumulating the results.

## Approach

- Initialized two static variables :
   - `mod` : A constant representing the modulus for performing modular arithmetic.
   - `jawab` : A static variable to store the final answer.

- Defined a static function `sequence` that takes an integer `n` as input and returns a long value.

- Inside the function :
   - Initialized `jawab` to 0, representing the cumulative result of the sequence.
   - Initialized a temporary variable `t` to 1, which is used for consecutive integer multiplication.

- Iterated from 1 to `n` :
   - Initialized a temporary variable `m` to 1, representing the product.
   - Used a counter `c` to perform `c` consecutive multiplications.
   - Multiplied `m` by `t`, update `t`, and take the result modulo `mod`.
   - Accumulated the result of `m % mod` to `jawab`, updating it with each iteration.

- After the loop, `jawab` contained the final result of the sequence.

- Returned the final result `jawab`.

My code effectively calculated the specified sequence by iteratively multiplying consecutive integers, taking care to use modular arithmetic to handle large results and prevent overflow.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n^2)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

$n$ : given input parameter 

- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 

```
// User function Template for Java

class Solution{
    
    // Static variables for modulus and the final answer
    static int mod = 1_000_000_007;
    static long jawab;

    // Function to calculate the sequence
    static long sequence(int n){
        
        // Initializing the answer variable
        jawab = 0;
        // Temporary variable for multiplication
        int t = 1;

        // Iterating from 1 to n
        for (int i = 1; i <= n; i++) {
            // Temporary variable for the product
            long m = 1;
            // Counter variable
            int c = i;

            // Calculating the product of t * (t + 1) * ... * (t + c - 1)
            while (c-- > 0) {
                m *= t;
                m %= mod;
                t++;
            }

            // Updating the final answer with the calculated product, modulo mod
            jawab = (jawab + m % mod) % mod;
        }

        // Returning the final answer
        return jawab;
    }
}     
```
