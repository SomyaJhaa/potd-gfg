## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 14-04-24

## [Xoring and Clearing](https://www.geeksforgeeks.org/problems/xoring-and-clearing/1)

## Intuition
The problem requires performing three tasks on an array :
- Calculate the bitwise XOR of each element in the array with its corresponding index.
- Print the resulting array.
- Set all elements of the array to zero.
- Print the resulting array.

## Approach

**Calculated XOR with Index :**
- I iterated through the array.
- For each element at index i, calculated the bitwise XOR of the element with i and updated the element in the array.
- This can be done in a single pass through the array.

**Print Array :**
- Iterated through the array and print each element.

**Set Elements to Zero :**
- Iterated through the array.
- Set each element to zero.

**Print Array Again :**
- Iterated through the array and print each element.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(a)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$a$ : size of the array
- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {

    // Function to print the array
    public void printArr(int n, int arr[]) {
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

    // Function to set all elements of the array to zero
    public void setToZero(int n, int arr[]) {
        for (int i = 0; i < n; i++) {
            arr[i] = 0; // Set each element to zero
        }
    }
    
    // Function to calculate the bitwise XOR of each element in the array with its corresponding index
    public void xor1ToN(int n, int arr[]) {
        for (int i = 0; i < n; i++) {
            arr[i] ^= i; // XOR each element with its index
        }
    }
}
```
