# 🎨🌈 Wishing You a Colorful Holi ! 🎉🎆
## May your journey through the repository be as bright and joyful as the colors of Holi ! Happy Holi to all our viewers ! 🌺💫

## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 25-03-24 

## [Print N-bit binary numbers having more 1s than 0s](https://www.geeksforgeeks.org/problems/print-n-bit-binary-numbers-having-more-1s-than-0s0252/1)

## Intuition
- My algorithm generates all possible binary strings of length N with a specific constraint.
- It starts with an empty binary string and recursively appends '1' or '0' based on the number of extra ones allowed.
- When all places are filled, it adds the binary string to the result list.

## Approach

- I initialized an empty list to store the generated binary strings.
- Defined a recursive function to generate binary strings:
   - Base case: If all places are filled, add the binary string to the result list.
   - Recursive step: Append '1' to the binary string and recursively call the function with one extra '1' allowed.
     If there are extra ones allowed, append '0' as well and recursively call the function with one fewer extra ones allowed.
- Started the recursion with an empty binary string and the allowed number of extra ones.
- Returned the list of generated binary strings.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( 2^N )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N$ : length of the binary strings
- Space complexity : $O( 2^N )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    static ArrayList<String> jawab;
    
    ArrayList<String> NBitBinary(int N) {
        // code here
        
        // Initialize jawab list
        jawab = new ArrayList<>();
        String binaryString = "";
        generate(binaryString, 0, N);
        return jawab;
    }
    
    static void generate(String binary, int extraOnes, int remainingPlaces) {
        // Base case : when all places are filled
        if (remainingPlaces == 0) {
            jawab.add(binary);
            return;
        }
        // Appending '1' and recursing
        generate(binary + "1", extraOnes + 1, remainingPlaces - 1);
        // If extraOnes is non-zero, appending '0' and recursing
        if (extraOnes > 0) {
            generate(binary + "0", extraOnes - 1, remainingPlaces - 1);
        }
    }
}	
```
