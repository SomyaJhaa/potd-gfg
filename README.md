## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 05-04-24 

## [Strictly Increasing Array](https://www.geeksforgeeks.org/problems/convert-to-strictly-increasing-array3351/1)

## Intuition
The problem aims to find the minimum number of operations required to make an array strictly increasing. To solve the problem, I can use dynamic programming.

## Approach
- I iterated through the array and for each element, we determine the length of the longest increasing subsequence ending at that element.
- I initialized a dynamic programming array 'dp' with all elements set to 1, indicating that initially each element forms a subsequence of length 1.
- I iterated over each element of the array:
  - For each element 'nums[i]', I iterate over the elements before it ('nums[j]' where 'j' ranges from 0 to 'i - 1').
  - If 'nums[i] > nums[j]' and the difference between 'nums[i]' and 'nums[j]' is greater than or equal to the difference in indices ('i - j'), it means I can include 'nums[i]' in the increasing subsequence ending at 'nums[i]'.
  - I updated the length of the longest increasing subsequence ending at 'nums[i]' by taking the maximum of the current value and '1 + dp[j]'.
  - I also updated a variable 'maxIncreasingLength' to keep track of the maximum increasing subsequence length encountered so far.
- Finally, I returned the difference between the length of the array and 'maxIncreasingLength', which represents the minimum number of operations required to make the array strictly increasing.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n^2)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : length of the input array `nums`

- Space complexity : $O(n)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    public int min_operations(int[] nums) {
        // Code here
        int length = nums.length;
        int maxIncreasingLength = 1;
        int[] dp = new int[length];
        
        // Initializing the dynamic programming array with 1s.
        for (int i = 0; i < length; i++)
            dp[i] = 1;
        
        // Performing dynamic programming to find the length of the longest increasing subsequence.
        for (int i = 1; i < length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j] && (nums[i] - nums[j] >= (i - j))) {
                    dp[i] = Math.max(1 + dp[j], dp[i]);
                    maxIncreasingLength = Math.max(maxIncreasingLength, dp[i]);
                }
            }
        }
        
        // Returning the minimum number of operations required to make the array strictly increasing.
        return length - maxIncreasingLength;
    }
}
```
