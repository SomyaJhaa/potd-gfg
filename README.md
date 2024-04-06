## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 06-04-24 

## [Count ways to N'th Stair](https://www.geeksforgeeks.org/problems/count-ways-to-nth-stairorder-does-not-matter1322/1)

## Intuition
The `countWays` function calculates the number of ways to reach the nth stair when the order doesn't matter.

## Approach

**Base Case** : If there's only one stair or none, there's only one way to reach it.

- For each additional stair :
   - I can either take one step.
   - Or skip the stair if `n` is even (since order doesn't matter).

- Thus, the total ways to reach the nth stair is `(n / 2) + 1`.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(1)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {

    // Function to count the number of ways to reach the nth stair
    // when the order does not matter.

    Long countWays(int n) {

        // Base case: if there is only one stair or no stair, there is only one way to reach it.
        long ways = 1;

        // For each stair, I can either take one step or skip it (if n is even).
        // So, the number of ways to reach the nth stair is (n/2) + 1.
        // I add 1 to account for the possibility of not taking any steps.
        ways += (n / 2);

        // Returning the total number of ways.
        return ways;
    }
}
```
