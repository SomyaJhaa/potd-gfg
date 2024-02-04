## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 03-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/decimal-equivalent-of-binary-linked-list/1)
## Decimal Equivalent of Binary Linked List

## Intuition

This problem involves converting a binary number represented by a linked list into its decimal equivalent. The linked list represents a binary number, where the significance of the bits decreases with increasing index in the linked list. The goal is to calculate the decimal value of this binary representation.

## Approach

**Calculated the Length of Linked List :**
   - Created a helper method `length` to calculate the length of the linked list.

**Traversed the Linked List :**
   - Traversed the linked list from the head to the tail.
   - For each node with a data value of 1, calculated the corresponding power of 2.
   - Updated the result by adding the calculated the power of 2, taking modulo `1_000_000_007` to prevent overflow.

**Modular Exponentiation :**
   - Created a helper method `modPow` for modular exponentiation.
   - Used binary exponentiation to efficiently calculate `base^exponent % MOD`.

**Returned the Result :**
   - Returned the final result, which represents the decimal value of the binary linked list.

My approach ensures that the conversion from binary to decimal is performed efficiently using modular arithmetic to handle large values and prevent overflow.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(l)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$l$ : length of the linked list

- Space complexity : $O(1)$ 
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 
```
/* Node of a linked list
 class Node {
   int data;
    Node next;
    Node(int d)  { data = d;  next = null; }
}
 Linked List class
class LinkedList
{
    Node head;  // head of list
}
This is method only submission.  You only need to complete the method. */

class Solution {
    
    // Modulo constant
    static int MOD = 1_000_000_007;

    // Method to calculate the decimal value of a binary linked list
    long DecimalValue(Node head) {
       
        // Calculating the length of the linked list
        int l = length(head) - 1;
        
        // Variable to store the final jawab
        long jawab = 0;
        
        // Temporary node pointer for traversing the linked list
        Node t = head;

        // Traverseing the linked list
        while (t != null) {
            // If the current node's data is 1, calculating the corresponding power of 2
            if (t.data == 1) {
                long powerOfTwo = modPow(2, l);
                // Updating the answer with the calculated power of 2
                jawab = (jawab + powerOfTwo) % MOD;
            }
            // Moving to the next node and decreasing the length
            l--;
            t = t.next;
        }
        // Returning the final answer
        return jawab;
    }

    // Method to calculate the length of a linked list
    static int length(Node head) {
        // Temporary node pointer for traversing the linked list
        Node t = head;
        // Variable to store the length
        int len = 0;
        
        // Traversing the linked list and count nodes
        while (t != null) {
            len++;
            t = t.next;
        }
        // Returning the calculated length
        return len;
    }

    // Method for modular exponentiation
    static long modPow(long base, int exponent) {
        // Variable to store the jawab of modular exponentiation
        long jawab = 1;
        
        // Calculating modular exponentiation using binary exponentiation
        while (exponent > 0) {
            if (exponent % 2 == 1) {
                jawab = (jawab * base) % MOD;
            }
            base = (base * base) % MOD;
            exponent /= 2;
        }
        // Returning the jawab of modular exponentiation
        return jawab;
    }
}
```

