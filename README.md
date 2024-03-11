🚀 Enjoy exploring my solution and keep the coding spirit alive! Happy coding ! ✨


## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 11-03-24 [Problem Link](https://www.geeksforgeeks.org/problems/count-pairs-sum-in-matrices4332/1)
## Count pairs Sum in matrices

## Intuition
My provided code defines a class `Solution` with a method `countPairs` that calculates the count of pairs from two matrices whose sum equals a given value `x`.

## Approach

##### Initialization :
- Initialized two HashSet objects, `h1` and `h2`, to store unique values from the first and second matrices, respectively.
- Initialized an integer variable `jawab` to store the count of pairs.

##### Populated the HashSets :
- Iterated through each element of the first matrix (`mat1`) and added its value to `h1`.
- Iterated through each element of the second matrix (`mat2`) and added its value to `h2`.

##### Counting Pairs :
- Iterated through the values in `h1`.
- For each value `v` in `h1`, checked if there exists a value in `h2` such that their sum equals the given value `x - v`.
- If such a value is found in `h2`, incremented the count (`jawab`) for each pair.

##### Result :
- The final count of pairs is stored in the variable `jawab`.

My approach ensured that unique values from both matrices are stored in separate HashSet objects, and then it iterated through one HashSet to check for pairs in the other HashSet whose sum equals the given value `x`.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( N1 + N2 )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N1$ : total number of elements in the first matrix

$N2$ : total number of elements in the second matrix
- Space complexity : $O( N1 + N2 )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // HashSet to store unique values from the first matrix
    static HashSet<Integer> h1;
    // HashSet to store unique values from the second matrix
    static HashSet<Integer> h2;
    // Variable to store the count of pairs
    static int jawab;

    // Method to count pairs from two matrices whose sum equals x
    int countPairs(int mat1[][], int mat2[][], int n, int x) {
    
        // Initializing HashSet h1 with unique values from the first matrix
        h1 = new HashSet<>();
        for (int i = 0; i < mat1.length; i++) {
            for (int j = 0; j < mat1[0].length; j++) {
                h1.add(mat1[i][j]);
            }
        }

        // Initializing HashSet h2 with unique values from the second matrix
        h2 = new HashSet<>();
        for (int i = 0; i < mat2.length; i++) {
            for (int j = 0; j < mat2[0].length; j++) {
                h2.add(mat2[i][j]);
            }
        }

        // Initializing jawab (count) to 0
        jawab = 0;

        // Iterating through values in h1
        for (int v : h1) {
            // Checking if there exists a value in h2 such that their sum equals x
            if (h2.contains(x - v)) {
                // Incrementing the count for each such pair
                jawab++;
            }
        }

        // Returning the final count of pairs
        return jawab;
    }
}
```
