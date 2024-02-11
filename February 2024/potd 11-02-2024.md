## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 11-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/recamans-sequence4856/1)
## Recamans sequence

## Intuition
The Recaman Sequence is a mathematical sequence defined by the following rules :
- Start with 0 as the first element.
- For each subsequent element at index 'i' :
    - If 'i' can be subtracted from the previous element resulting in a positive number not already present, subtract 'i'.
    - Otherwise, add 'i' to the previous element.

## Approach

**Initialization :**
- Created an ArrayList (`jawab`) to store the Recaman sequence.
- Initialized a HashSet (`h`) to efficiently check for the existence of elements.

**Base Case :**
- If the requested length `n` is 0, returned an empty ArrayList as there are no elements to generate.

**Sequence Generation :**
- Started with 0 as the first element and added it to both the ArrayList and HashSet.
- Iterated from 1 to `n-1` to generated the subsequent elements in the sequence.
- For each iteration :
  - Calculated the potential next element by subtracting `i` or adding `i` to the previous element.
  - Checked if the calculated value is valid (greater than 0) and not already present in the HashSet.
  - If valid, added the element to both the ArrayList and HashSet; otherwise, used the addition operation.

**Returned the Result :**
- Returned the generated Recaman sequence stored in the ArrayList.

### Summary :
My approach involved a systematic generation of elements in the Recaman sequence, adhering to specific rules at each step. Efficient element existence checked using a HashSet prevented duplicates in the sequence. The final result is the Recaman sequence stored in an ArrayList.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

$n$ : given

- Space complexity : $O(n)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 

```
//User function Template for Java

class Solution {
    static ArrayList<Integer> jawab; // ArrayList to store the Recaman sequence
    static HashSet<Integer> h; // HashSet to efficiently check for element existence

    static ArrayList<Integer> recamanSequence(int n) {
        
        // Checking if n is 0, return an empty ArrayList
        if (n == 0) {
            return new ArrayList<>();
        }

        // Initializing ArrayList and HashSet
        jawab = new ArrayList<>();
        h = new HashSet<>();

        // Initializing the sequence with 0
        jawab.add(0);
        h.add(0);

        // Generating the Recaman sequence
        for (int i = 1; i < n; i++) {
            int p = jawab.get(i - 1);

            // Calculating the next element in the sequence
            int subtract = p - i;
            
            // Checking if the subtracted value is valid and not already in the HashSet
            if (subtract > 0 && !h.contains(subtract)) {
                jawab.add(subtract);
                h.add(subtract);
            } else {
                // If not, using the addition operation
                int add = p + i;
                jawab.add(add);
                h.add(add);
            }
        }

        // Returning the generated Recaman sequence
        return jawab;
    }
}         
```
