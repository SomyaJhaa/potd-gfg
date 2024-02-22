## GeeksForGeeks Problem Of The Day Solutions

## Today's 22-02-24 
## [Distinct occurrences](https://www.geeksforgeeks.org/problems/distinct-occurrences/1)

## Intuition


This problem aimed to find the count of subsequences of string `t` in string `s`. A subsequence is a sequence of characters that appears in the same order but not necessarily consecutively.


## Approach

**Initialization :**
   - Initialized static variables `sh` and `th` to store input strings `s` and `t`.
   - Created a memoization array `gp` to store intermediate results, initialized with -1.
   - Set the modulo value `m` to 1,000,000,007.

**Recursive Helper Function :**
   - Defined a recursive helper function `helper(i, j)` to calculate the count of subsequences starting from indices `i` and `j` in strings `s` and `t`, respectively.
   - Base Cases:
     - If the remaining characters in `t` are more than the remaining characters in `s`, returned 0.
     - If all characters in `t` are processed, returned 1 (subsequence found).
     - If all characters in `s` are processed, returned 0 (subsequence not found).

**Memoization :**
   - Used the memoization array `gp` to store and retrieved already calculated results to avoid redundant calculations.

**Recursive Calls :**
   - If the current characters in `s` and `t` match, recursively calculated for both including and excluding the character in `s`.
   - If the characters do not match, recursively calculated for excluding the character in `s`.

**Result :**
   - The result of the helper function with the initial indices (0, 0) represented the total count of subsequences of `t` in `s`.

**Modulo Operation :**
   - Applied modulo operation `% m` to handle large values and prevent overflow.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n*m)$ 
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  length of string `s`

$m$ :  length of string `t`
- Space complexity : $O(n*m)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
   
## Code 

```
//User function Template for Java

/* You are required to complete this method */

class Solution {
   
    // Static variables to store the input strings and memoization array
    static String sh;
    static String th;
    static int[][] gp;
    static int m = 1_000_000_007;

    // Method to calculate the count of subsequences
    int subsequenceCount(String s, String t) {
       
       // Initializing static variables with input strings
        sh = s;
        th = t;
        
        // Initializing memoization array
        gp = new int[s.length() + 1][t.length() + 1];

        // Filling the memoization array with -1
        for (int i = 0; i < s.length() + 1; i++) {
            Arrays.fill(gp[i], -1);
        }

        // Calling the helper function to perform the calculation
        return helper(0, 0);
    }

    // Helper function to perform the recursive calculation
    static int helper(int i, int j) {
        // Base case : If the remaining characters in t are more than the remaining characters in s, returning 0
        if (th.length() - j > sh.length() - i) {
            return 0;
        }

        // Base case : If all characters in t are processed, returning 1 (subsequence found)
        if (j == th.length()) {
            return 1;
        }

        // Base case : If all characters in s are processed, returning 0 (subsequence not found)
        if (i == sh.length()) {
            return 0;
        }

        // If the result is already calculated, returning it
        if (gp[i][j] != -1) {
            return gp[i][j];
        }

        // If the current characters match, recursively calculating for both including and excluding the character
        if (sh.charAt(i) == th.charAt(j)) {
            return gp[i][j] = (helper(i + 1, j + 1) % m + helper(i + 1, j) % m) % m;
        }

        // If the current characters do not match, recursively calculating for excluding the character in s
        return gp[i][j] = (helper(i + 1, j)) % m;
    }
}
```
