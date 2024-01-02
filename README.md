#  Problem Of The Day Solutions GeeksForGeeks

## Today's 02-01-24 [Problem Link](https://www.geeksforgeeks.org/problems/largest-sum-subarray-of-size-at-least-k3121/1)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Kadane's algorithm

# Approach
<!-- Describe your approach to solving the problem. -->
- I simply applied Kadane's algorithm
- Stored the initial sum
- Trversed the array and kept track of elements from starting as well
- Updated the answer if got maximum till now
---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

# Complexity
- Time complexity : $$O(n)$$
$$l$$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $$O(1)$$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
// User function Template for Java

class Solution {
    
    public long maxSumWithK(long a[], long n, long k){
        long jor = 0;    // to store the sum
        long b = 0;     // to keep track of left sum
        int ib = 0;    // to keep track of current leftsum index
        for( int i = 0; i < (int)k; i++){
            jor += a[i];
        }
        long jawab = Math.max( jor, Long.MIN_VALUE);
        
        for( int i = (int)k; i < (int)n; i++){
            jor += a[i];
            b += a[ib++];
            jawab = Math.max(jawab, jor);
            if( b < 0){
                jor -= b;
                jawab = Math.max(jawab, jor);
                b = 0;
            }
        }
        return jawab;
    }
}
```
