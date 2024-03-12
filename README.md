## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 12-03-24 

## [Generalised Fibonacci numbers](https://www.geeksforgeeks.org/problems/generalised-fibonacci-numbers1820/1)

## Intuition
The goal of my algorithm should be to efficiently calculate the Fibonacci number modulo m using matrix exponentiation. 

## Approach

The approach involved representing the Fibonacci transformation as a matrix and then using binary exponentiation to compute the matrix power.

**Identity Matrix Initialization :**
   - Initialized a static 3x3 matrix `hm` representing the identity matrix.

**genFibNum Function :**
   - Defined a function `genFibNum` that takes the coefficients a, b, c, the target Fibonacci term `n`, and the modulo value `m`.
   - Base Case : If `n` is less than or equal to 2, returned 1.
   - Initialized the matrix `h1` with the identity matrix `hm`.
   - Initialized the transformation matrix `h2` with the given coefficients.
   - Subtracted 2 from `n` as the base cases are already handled.
   - Used binary exponentiation to calculate `h1 = h2^n % m`.
   - Calculated the sum of the first row of the resulting matrix `h1` modulo `m` and returned the result.

**multiplyMatrices Function :**
   - Defined a helper function `multiplyMatrices` to perform matrix multiplication modulo `m`.
   - Iterated through the matrices `mat1` and `mat2` to calculate the product, considering the modulo operation.

My algorithm leveraged matrix exponentiation to efficiently compute the Fibonacci number modulo `m`, providing a scalable and optimized solution for large Fibonacci terms.


---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( log n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : target Fibonacci term

- Space complexity : $O( 1 )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Static matrix representing the identity matrix
    static long[][] hm = {
        {1, 0, 0},
        {0, 1, 0},
        {0, 0, 1}
    };

    // Function to calculate Fibonacci number modulo m
    static long genFibNum(Long a, Long b, Long c, long n, long m) {
       
        // Base case: return 1 if n is 1 or 2
        if (n <= 2) {
            return 1;
        }

        // Initializing the matrix h1 with the identity matrix
        long[][] h1 = hm;

        // Initializing the transformation matrix h2
        long[][] h2 = {
            {a, b, c},
            {1, 0, 0},
            {0, 0, 1}
        };

        // Subtracting 2 from n as the base cases are already handled
        n -= 2;

        // Performing matrix exponentiation using binary exponentiation
        while (n > 0) {
            if ((n & 1) == 1) {
                h1 = multiplyMatrices(h1, h2, m);
            }
            h2 = multiplyMatrices(h2, h2, m);
            n >>= 1;
        }

        // Calculating the sum of the first row of the resulting matrix modulo m
        long result = 0;
        for (long value : h1[0]) {
            result = (result + value) % m;
        }

        return result;
    }

    // Helper function to multiply two matrices modulo m
    static long[][] multiplyMatrices(long[][] mat1, long[][] mat2, long m) {
        int rows = mat1.length;
        int cols = mat2[0].length;
        long[][] result = new long[rows][cols];

        // Performing matrix multiplication
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                for (int k = 0; k < mat1[0].length; k++) {
                    result[i][j] = (result[i][j] + (mat1[i][k] * mat2[k][j]) % m) % m;
                }
            }
        }

        return result;
    }
}
```
