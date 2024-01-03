#  Problem Of The Day Solutions GeeksForGeeks

## Today's 03-01-24 [Problem Link](https://www.geeksforgeeks.org/problems/smallest-window-containing-0-1-and-2--170637/1)

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The goal is to find the smallest substring that contains all three characters '0', '1', and '2'. The code uses three variables (i0, i1, i2) to keep track of the last indices where each of these characters was encountered. The main loop iterates through the string, updating these indices and calculating the length of the substring whenever all three characters are found.

# Approach
<!-- Describe your approach to solving the problem. -->
- Initialize three variables (i0, i1, i2) to -1, representing the last indices of characters '0', '1', and '2' in the string.
- Initialize a variable m to INT_MAX, which will be used to store the length of the smallest substring.
- Use a boolean variable teenomilgye to indicate whether all three characters have been encountered.
- Iterate through the string (S) using a for loop.
- - Update the indices i0, i1, and i2 when encountering '0', '1', and '2', respectively.
- - If all three characters are encountered (teenomilgye is true), calculate the length of the current substring and update m with the minimum length.
- After the loop, check if all three characters have been encountered (teenomilgye is true). If yes, return the minimum length (m), otherwise, return -1 indicating that no such substring was found.

# Complexity
- Time complexity : $$O(n)$$
$$n$$ : length of given array
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity : $$O(1)$$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```
#include <string>
#include <climits>
#include <algorithm> 
class Solution {
  public:
    int smallestSubstring(string S) {
        // Code here
        int i0 = -1;
        int i1 = -1;
        int i2 = -1;
        int m = INT_MAX;
        bool teenomilgye = false;
        for( int i = 0; i < S.size(); i++){
            if( S[i] == '0'){
                i0 = i;
            }
            else if( S[i] == '1'){
                i1 = i;
            }
            else if( S[i] == '2'){
                i2 = i;
            }
            
            if( i0 != -1 && i1 != -1 && i2 != -1) {
                teenomilgye = true;
            }
            
            if( teenomilgye){
                int maxindex = max( {i0, i1, i2});
                int minindex = min( {i0, i1, i2});
                int d = maxindex - minindex + 1;
                m = min(m, d);
            }
        }
        if( teenomilgye){
            return m;
        }
        return -1;
    }
};
```
