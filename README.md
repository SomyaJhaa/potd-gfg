## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 13-04-24

## [Reverse Bits](https://www.geeksforgeeks.org/problems/reverse-bits3556/1)

## Intuition
Given a number `x`, I aim to reverse its binary representation and return the result in decimal form.

## Approach

**Iterated over Bits** : 
- I iterated over the 32 bits of `x`.
- For each bit, right shift `x` to obtain the rightmost bit, then left shift the result by 1 and add the obtained bit.

**Result** : 
- The result after iterating over all bits is the reversed binary representation of `x` in decimal form.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(log(x))$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$x$ : given
- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    static Long reversedBits(Long x) {
        
        long jawab = 0;
        for (int i = 0; i < 32; i++) {
            
            // Get the rightmost bit of x and add it to jawab
            jawab = (jawab << 1) | (x & 1);
            
            // Right shift x to get the next bit
            x >>= 1;
        }
        return jawab;
    }
};
```
