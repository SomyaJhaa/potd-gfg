# GeeksForGeeks Problem Of The Day Solutions

This is my attemp to make the coding experience easier for you guys so that you can easily learn what to do in today's leetcode challenge.


## A very Happy Near Year to all you guys, may god give you strength to overcome what you want.
## Always here to assist you guys.

## Todays 01-01-24 [Problem Link](https://www.geeksforgeeks.org/problems/array-pair-sum-divisibility-problem3257/1)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Remainder storing.

# Approach
<!-- Describe your approach to solving the problem. -->
- I created a helper array to store the remainders ( as possible remainders will be from 0 to 'k-1')
- - filled it with a for loop iteration
- Checked every remainder in 'help' array
- - if the remainder and its complementary both aren't same , then also it would be impossible to divide them in pairs
                return false;
---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

# Complexity
- Time complexity : $$O(l)$$
$$l$$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $$O(k)$$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
// User function Template for Java

class Solution {
    public boolean canPair(int[] nums, int k) {
        // Code here
        int[] help = new int[k];  // to store the count of remainders ( as possible remainders will be from 0 to 'k-1')
        for( int a : nums){
            int t = a % k;
            if( t < 0){     // in case if remainder is negative ( in case of negative 'a')
                t += k;
            }
            help[t]++;
        }

        if( help[0] % 2 != 0){  // as if there will be odd number of '0' remainder then it would be impossible to divide them in pairs
            return false;
        }
        
        for( int i = 1; i <= k/2; i++){
            if(  help[k-i] != help[i]){  // if the remainder and its complementary both aren't' , then also it would be impossible to divide them in pairs
                return false;
            }
        }
        return true;
    }
}
```
