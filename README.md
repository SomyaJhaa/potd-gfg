# 🎨🌈 Wishing You a Colorful Holi ! 🎉🎆
## May your journey through the repository be as bright and joyful as the colors of Holi ! Happy Holi to all our viewers ! 🌺💫

## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 26-03-24 

## [Additive sequence](https://www.geeksforgeeks.org/problems/additive-sequence/1)

## Intuition
An additive sequence is a series of numbers in which each number in the sequence is the sum of the two preceding numbers. The idea behind the algorithm is to explore all possible combinations of the first two numbers in the sequence and then recursively check if the remaining string forms a valid additive sequence.

## Approach

**Input Validation :** I checked if the length of the input string is less than or equal to 2. If so, return false as an additive sequence must contain at least three numbers.
- **Initialization :** Initialized two static variables `jawab` (result) and `sequence` (to store the current sequence being checked).
- **Recursion :** Defined a recursive function `checkAdditive` that takes the input string and the starting index as parameters.
- **Base Case :** If the starting index equals the length of the input string and the size of the sequence is greater than 2, set the result to true.
- **Updated Variables :** Updated variables `first`, `second`, and `current` based on the current state of the sequence.
- **Iterated :** Iterated through the remaining characters in the input string starting from the current index.
- **Backtracking :** Added the current number to the sequence if the sequence size is less than 2 and the result is not true. Recursively call the `checkAdditive` function with the updated parameters. Removed the current number from the sequence to backtrack and explore other possibilities.
- **Checked Conditions :** Checked if the current number violates the additive property or if it satisfies the additive property. Return or continue accordingly.
- **Result :** After exploring all possibilities, returned the final result.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( N^2 )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$N$ : length of the input string
- Space complexity : $O( N )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Static variables to store the result and the sequence being checked
    static boolean jawab;
    static ArrayList<Integer> sequence;

    // Method to check if the given string forms an additive sequence
    public boolean isAdditiveSequence(String n) {
        
        // Checking if the length of the input string is less than or equal to 2
        if (n.length() <= 2) {
            return false;
        }
        
        // Initializing the result and sequence
        jawab = false;
        sequence = new ArrayList<>();
        
        // Invoking the recursive method to check for additive sequence
        checkAdditive(n, 0);
        
        // Returning the result
        return jawab;
    }

    // Recursive method to check for additive sequence
    static void checkAdditive(String input, int startIndex) {
        
        // If we have processed the entire string and the sequence contains more than 2 numbers, set the result to true
        if (startIndex == input.length() && sequence.size() > 2) {
            jawab = true;
            return;
        }

        // Variables to store the first, second, and current numbers in the sequence
        int first = 0, second = 0, current = 0;
        
        // If the sequence has at least 2 numbers, updating the first and second numbers
        if (sequence.size() >= 2) {
            second = sequence.get(sequence.size() - 1);
            first = sequence.get(sequence.size() - 2);
        }

        // Iterating through the remaining characters in the string
        for (int i = startIndex; i < input.length(); i++) {
            
            // Updating the current number by appending digits from the input string
            current = current * 10 + (input.charAt(i) - '0');
            
            // If the sequence has less than 2 numbers and the result is not yet true, try adding the current number to the sequence
            if (sequence.size() < 2 && !jawab) {
                sequence.add(current);
                // Recursively checking the rest of the string starting from the next index
                checkAdditive(input, i + 1);
                // Removing the current number from the sequence to backtrack
                sequence.remove(sequence.size() - 1);
            } 
            
            // If the current number is greater than the sum of the first and second numbers and the result is not yet true, return
            else if (current > (first + second) && !jawab) {
                return;
            } 
            
            // If the current number is equal to the sum of the first and second numbers and the result is not yet true, try adding the current number to the sequence
            else if (current == first + second && !jawab) {
                sequence.add(current);
                // Recursively checking the rest of the string starting from the next index
                checkAdditive(input, i + 1);
                // Removing the current number from the sequence to backtrack
                sequence.remove(sequence.size() - 1);
            }
        }
        return;
    }
}	
```
