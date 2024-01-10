#  Problem Of The Day Solutions GeeksForGeeks

## Today's 10-01-24 
## [Longest subarray with sum divisible by K](https://www.geeksforgeeks.org/problems/longest-subarray-with-sum-divisible-by-k)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem asks for the length of the longest subarray with a sum divisible by K. The cumulative sum approach and the use of a HashMap can be applied to efficiently solve this problem.

# Approach:

- Initialize a variable longest to store the length of the longest subarray.
- Use a HashMap (unordered_map in C++) to store the remainder and its corresponding index while iterating through the array.
- Initialize a variable add to store the cumulative sum.
- Iterate through the array, and for each element, update the cumulative sum (add).
- Calculate the remainder after dividing the cumulative sum by K.
- If the remainder is 0, update the longest to the current index (i + 1).
- If the remainder is already present in the HashMap, update the longest to the difference between the current index (i) and the index stored in the HashMap for that remainder.
- If the remainder is not present, add it to the HashMap along with its index.
- After the iteration, return the longest as the result.

# Complexity
- Time complexity : $O(N)$

 $N$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $O(N)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
class Solution{
public:	
	int longSubarrWthSumDivByK(int arr[], int n, int k)
	{
	    // Initialized the variable to store the length of the longest subarray
        int longest = 0;
        
        // HashMap to store the remainder and its corresponding index
        unordered_map<int, int> m;
        
        // Variable to store the cumulative sum
        int add = 0;

        // Iterated through the array
        for (int i = 0; i < n; i++) {
            // Update the cumulative sum
            add += arr[i];
            
            // Calculated the remainder after dividing the cumulative sum by k
            int remainder = ((add % k) + k) % k;
            
            // Checked if the cumulative sum is divisible by k
            if (remainder == 0) {
                // Updated the length of the longest subarray
                longest = i + 1;
            } else if (m.count(remainder) > 0) {
                // If the remainder is already present in the HashMap, updated the longest subarray length
                longest = max(longest, i - m[remainder]);
            } else {
                // If the remainder is not present, added it to the HashMap along with its index
                m[remainder] = i ;
            }
        }

        // Returned the length of the longest subarray
        return longest;
	}
};

```
