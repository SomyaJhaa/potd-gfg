# Happy Holika Dahan! May the flames of this sacred fire ignite hope, love, and prosperity in your life. 🪔✨ #HolikaDahan

## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 24-03-24 

## [Insert an Element at the Bottom of a Stack](https://www.geeksforgeeks.org/problems/insert-an-element-at-the-bottom-of-a-stack/1)

## Intuition
The intuition behind this method is to use an additional stack to reverse the order of elements in the original stack temporarily. This allows to insert the new element at the bottom of the stack efficiently.

## Approach

- Created a temporary stack (`tempStack`) to hold elements temporarily.
- Popped all elements from the original stack (`st`) and push them onto the temporary stack. This effectively reverses the order of elements in the original stack.
- Pushed the new element (`x`) onto the original stack (`st`). This effectively inserts the new element at the bottom of the original stack.
- Popped all elements from the temporary stack (`tempStack`) and push them back onto the original stack (`st`). This restores the original order of elements.
- Returned the modified original stack (`st`) with the new element inserted at the bottom.

By following this approach, I can efficiently insert an element at the bottom of the stack while maintaining the order of other elements.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of elements in the stack
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Method to insert an element at the bottom of a stack
    public Stack<Integer> insertAtBottom(Stack<Integer> st, int x) {
        
        // Creating a temporary stack to hold elements temporarily
        Stack<Integer> tempStack = new Stack<>();
        
        // Pushing all elements from the original stack to the temporary stack
        while (!st.isEmpty()) {
            tempStack.push(st.pop());
        }
        
        // Pushing the new element to the original stack, effectively inserting it at the bottom
        st.push(x);
        
        // Popping all elements from the temporary stack and push them back to the original stack
        while (!tempStack.isEmpty()) {
            st.push(tempStack.pop());
        }
        
        // Returning the modified original stack with the new element inserted at the bottom
        return st;
    }
} 	
```
