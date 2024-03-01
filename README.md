## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 01-03-24 [Problem Link](https://www.geeksforgeeks.org/problems/peak-element/1)
## Peak element

## Intuition
The goal is to find a peak element in the given array. A peak element is an element that is greater than or equal to its neighbors. The code uses a binary search approach to efficiently locate a peak element.

## Approach

 **Binary Search :**
   - I initialized the pointers `l`, `r`, and `m` for binary search. `l` points to the start of the array, `r` points to the end, and `m` represents the middle index.
   - Performed a binary search until a peak element is found.
  
**Checked for Peak Element :**
   - At each step, checked if the element at index `m` is a peak.
   - A peak element must be greater than or equal to its neighbors (if they exist).

**Updated Search Space :**
   - If the middle element is not a peak, adjusted the search space based on the comparisons with its neighbors.
     - If the element to the left of `m` is greater, searched in the left half.
     - If the element to the right of `m` is greater or equal, searched in the right half.

**Break Condition :**
   - Break out of the binary search loop when a peak element is found (the conditions for a peak are satisfied).

**Returned Peak Index :**
   - Returned the index `m` as the result, representing the index of the peak element.

The binary search efficiently reduces the search space in each iteration, making the algorithm more time-efficient.

My code ensured that it finds a valid peak element by considering edge cases at the boundaries of the array.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( log n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
// User function Template for Java

/*Complete the function below*/

class Solution {
    // Function to find the peak element
    // arr[]: input array
    // n: size of array a[]
    
    public int peakElement(int[] arr, int n) {
        
        // Initializing pointers for binary search
        int l = 0;
        int r = n - 1;
        int m = 0; // Variable to store the middle index

        // Performing binary search to find the peak element
        while (l <= r) {
            
            // Calculating the middle index using bitwise right shift (equivalent to dividing by 2)
            m = (l + r) >> 1;

            // Checking if the middle element is a peak (greater than or equal to its neighbors)
            if ((m == 0 || arr[m - 1] <= arr[m]) && (m == n - 1 || arr[m + 1] <= arr[m])) {
                // If it's a peak, break out of the loop
                break;
            }

            // If the element to the left of the middle is greater, searching in the left half
            if (m > 0 && arr[m - 1] > arr[m]) {
                r = m - 1;
            } else {
                // If the element to the right of the middle is greater or equal, searching in the right half
                l = m + 1;
            }
        }

        // Returning the index of the peak element
        return m;
    }
}
```
