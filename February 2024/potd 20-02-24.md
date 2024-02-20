## GeeksForGeeks Problem Of The Day Solutions

## Today's 20-02-24 
## [Word Break](https://www.geeksforgeeks.org/problems/word-break1352/1)

## Intuition
The goal of this problem is to determine if a given string `s` can be broken into words from a provided dictionary.

## Approach

**HashSet Initialization :**
   - Created a HashSet (`h`) to store dictionary words for quick lookup.

**Dictionary Population :**
   - Iterated through the given `dictionary` and added each word to the HashSet.

**Recursive Break Check :**
   - Used a recursive function (`bnsktakya`) to check if the input string can be broken.
   - Base case : If the input string is empty, returned true (it can always be broken).
   - Iterated through the characters of the string, accumulating them in a temporary string.
   - If the accumulated string is in the dictionary and the remaining part can also be broken recursively, returned true.

**Result :**
   - If the `bnsktakya` function returns true, the original string can be broken, and the function returns 1.
   - Otherwise, it returns 0.

My approach leverages HashSet for efficient word lookup and recursion to explore possible word breaks in the input string.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(2^s)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$s$ :  length of the input string
- Space complexity : $O(s)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
   
## Code 

```
// User function Template for Java

class Solution
{
    // HashSet to store the dictionary words for quick lookup
    static HashSet<String> h;

    // Main function to check if the input string can be broken into words from the dictionary
    public static int wordBreak(int n, String s, ArrayList<String> dictionary ){
        
        // Initializing the HashSet with dictionary words
        h = new HashSet<>();
        for( String str : dictionary ){
            h.add(str);
        }
        
        // Checking if it is possible to break the input string
        if( bnsktakya(s)){
            return 1; // Returning 1 if possible
        }
        return 0; // Returning 0 if not possible
    }
    
    // Recursive function to check if the string can be broken into words
    static boolean bnsktakya( String s){
        // Base case: an empty string can always be broken
        if( s.length() == 0){
            return true;
        }

        // Temporary string to accumulate characters
        String temp = "";

        // Iterating through the characters of the string
        for( int i = 0; i < s.length(); i++){
            // Appending the current character to the temporary string
            temp += s.charAt(i);

            // Checking if the accumulated string is in the dictionary, and if the remaining part can also be broken
            if( h.contains(temp) && bnsktakya(s.substring(i+1))){
                return true; // Return true if it can be broken
            }
        }

        return false; // Returning false if no valid break is found
    }
}
```
