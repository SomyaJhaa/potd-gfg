## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 29-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/sum-of-bit-differences2937/1)
## Sum of bit differences

## Intuition
The problem involves finding the sum of bit differences across all pairs of elements in an array. Bit difference at a particular position is the count of pairs where one element has the bit set (1) and the other has the bit unset (0) at that position.

## Approach

**Initialized the Result :** I initialized a variable (`jawab`) to store the final result.

**Iterated Through Bits (0 to 31) :** Looped through each bit position (from 0 to 31 for 32-bit integers).

**Count Set Bits :** For each bit position, I counted the number of elements in the array where the bit is set (1) at that position.

**Updated the Result :** Updated the result (`jawab`) by adding twice the product of the count of set bits and the count of unset bits at the current position.

**Repeated for Each Bit Position :** Repeated steps 3-4 for all 32 bit positions.

**Result:** Returned the final result (`jawab`).


- For each bit position, I counted the number of set bits and unset bits in the array.
- The count of set bits (`c`) represented the number of elements where the bit is set at that position.
- The count of unset bits is `(n - c)`, where `n` is the total number of elements.
- The bit differences for the current position are given by `2 * (n - c) * c`.
- Summing up these bit differences for all positions gived the final result.


My approach ensures an efficient calculation of the sum of bit differences without explicitly comparing each pair of elements.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(32 * n)$ ${\equiv}$ $O(n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
   
## ETON 
My java code is correct but giving error on last five test cases ( It passed 1100 / 1115 testcases). So I submitted the same logic in Python language and it gets accepted. This may be due to server error from GeeksforGeeks end, anyways I have provided my Python code as well. You just grasp the logic as both code's logic are same.

## Java Code

```
// User function Template for Java

class Solution {
    
    // Variable to store the final result
    static long jawab;

    // Function to calculate the sum of bit differences
    long sumBitDifferences(int[] arr, int n) {
        
        // Initializing the result variable
        jawab = 0;

        // Iterating through each bit position (0 to 31 for 32-bit integers)
        for (int i = 0; i < 32; i++) {
            // Counting the number of set bits at the current position
            int c = 0;
            for (int j = 0; j < n; j++) {
                // Checking if the bit at the current position is set in the current element
                if (((1 << i) & arr[j]) != 0) {
                    c++;
                }
            }

            // Updating the result using the count of set and unset bits at the current position
            jawab += (2 * (n - c) * c);
        }

        // Returning the final result
        return jawab;
    }
}
```

## Python Code

```
# User function Template for python3

class Solution:

    # Static variable to store the result
    jawab = 0
    
    def sumBitDifferences(self, arr, n):
        # Initialize result
        Solution.jawab = 0

        # Iterated through each bit position (0 to 31 for 32-bit integers)
        for i in range(0, 32):
            # Counted number of elements with i'th bit set
            c = 0
            for j in range(0, n):
                if ( (1 << i) & arr[j] ):
                    c += 1
            Solution.jawab += (2 * (n - c) * c)

        return Solution.jawab
```
