## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 19-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/game-with-string4100/1)
## Game with String

## Intuition
The task is to find the minimum sum of squares of characters in the string after performing at most `k` removals. The character frequencies play a crucial role in determining the contribution to the sum, and the goal is to minimize this sum.

## Approach

**Initialized the Variables :**
   - `maxF` : Variable to store the maximum frequency encountered.
   - `m` : HashMap to store character frequencies.
   - `sco` : Array to store frequency counts.

**Counted Character Frequencies :**
   - Iterated through the characters in the input string `s`.
   - Updated the frequency count in the HashMap `m`.
   - Kept track of the maximum frequency encountered (`maxF`).

**Initialized the Frequency Count Array (`sco`) :**
   - Created an array `sco` with a size of `s.length() + 1` to store frequency counts.
   - Counted the occurrences of each frequency in the HashMap and updated the `sco` array.

**Performed Removals :**
   - While `k` is greater than 0 :
     - Identified the count of characters with the maximum frequency (`sbsejada`).
     - If `sbsejada` is less than or equal to `k`, performed removals and updated the `sco` array.
     - If `sbsejada` is greater than `k`, partially removed characters with the maximum frequency and updated `sco`.
     - Broke the loop as the required removals are completed.

**Calculated Minimum Sum of Squares :**
   - Iterated through the `sco` array and calculated the minimum sum of squares based on the frequency counts.

**Returned the Result :**
   - Returned the calculated minimum sum of squares.

My approach utilized a HashMap to efficiently count character frequencies and an array (`sco`) to keep track of the counts of different frequencies. Removals were performed based on the maximum frequency encountered, ensuring the minimum sum of squares is achieved.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(s)$
  - $s$ : number of nodes in the tree
<!-- Add your time complexity here, e.g. $$O())$$ -->
$s$ : length of the string
- Space complexity : $O(u)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$u$ : unique characters
   
## Code 

```
// User function Template for Java

class Solution {
    
    static int maxF;  // Variable to store the maximum frequency
    static HashMap<Character, Integer> m;  // HashMap to store character frequencies
    static int[] sco;  // Array to store frequency counts
    
    static int minValue(String s, int k) {
        
        // Initializing maxF and HashMap
        maxF = 0;
        m = new HashMap<>();
        
        // Counting character frequencies and update maxF
        for (char c : s.toCharArray()) {
            m.put(c, m.getOrDefault(c, 0) + 1);
            maxF = Math.max(maxF, m.get(c));
        }
        
        // Initializing sco array with size + 1
        sco = new int[s.length() + 1];
        
        // Counting frequency occurrences and update sco array
        for (int v : m.values()) {
            sco[v]++;
        }
        
        // Performing removals until k becomes 0
        while (k > 0) {
            int sbsejada = sco[maxF];
            if (sbsejada <= k) {
                // If the count of characters with maximum frequency is less than or equal to k,
                // performing removals and updating the sco array
                k -= sbsejada;
                sco[maxF - 1] += sbsejada;
                sco[maxF] = 0;
                maxF--;
            } else {
                // If the count of characters with maximum frequency is greater than k,
                // partially removing them and updated the sco array
                sco[maxF] -= k;
                maxF--;
                sco[maxF] += k;
                break;
            }
        }
        
        int jawab = 0;
        
        // Calculating the minimum sum of squares
        for (int i = 0; i < s.length() + 1; i++) {
            jawab += (i * i) * sco[i];
        }
        
        return jawab;
    }
}
```
