## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 31-03-24 

## [Closest Neighbour in BST](https://www.geeksforgeeks.org/problems/closest-neighbor-in-bst/1)

## Intuition
I utilized the properties of a binary search tree (BST) to efficiently find the greatest number less than or equal to the target value.

## Approach
- Started with the root node of the BST.
- Traversed down the BST, comparing node values with the target value.
- Updated the maximum value found so far if a node's value is less than or equal to the target.
- Continued traversal until reaching a leaf node or a node with no valid children.
- Returned the maximum value found, representing the greatest number in the BST less than or equal to the target.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(h)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$h$ : height of the tree

However, in the average case, when the tree is balanced, the time complexity is $O(log n)$, where $n$ is the number of nodes in the BST.
- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

/*class Node
{
    int key;
    Node left, right;

    Node(int x)
    {
        key = x;
        left = right = null;
    }

}*/

class Solution {

    // Function to find the greatest number in the binary search tree (BST) 
    // that is less than or equal to n.

    public static int findMaxForN(Node root, int n) {
        
        // Initializing the maximum value found so far
        int maxVal = Integer.MIN_VALUE;
        
        // Traversing down the BST until reaching a leaf node or a node with no valid children
        while (root != null) {
            // If the current node's value is less than or equal to n
            if (root.key <= n) {
                // Updating maxVal if the current node's value is greater than the current maxVal
                maxVal = Math.max(maxVal, root.key);
                // Moving to the right subtree to potentially find a greater value
                root = root.right;
            } else {
                // If the current node's value is greater than n, moving to the left subtree
                root = root.left;
            }
        }
        
        // If maxVal remains the default value, returning -1 indicating no valid value found
        return maxVal == Integer.MIN_VALUE ? -1 : maxVal;
    }
}
```
