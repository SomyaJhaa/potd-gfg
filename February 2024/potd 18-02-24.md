## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 18-02-24 [Problem Link](https://www.geeksforgeeks.org/problems/sum-of-leaf-nodes-in-bst/1)
## Sum of leaf nodes in BST

## Intuition
- To calculate the sum of leaf nodes, I need to traverse the binary search tree and identify the leaf nodes.
- A leaf node is a node with no left and right children.

## Approach

- I initialized a global variable `jawab` to store the sum of leaf nodes.
- Created a main function `sumOfLeafNodes` that takes the root of the binary search tree as input.
- Reset the `jawab` variable before each function call.
- Called a helper function, say `helper`, passing the root of the binary search tree.
- Inside the `helper` function :
   - Base case : If the current node is null, return.
   - Recursively called `helper` for the left and right subtrees.
   - If the current node is a leaf node (both left and right children are null), added its data to the `jawab` variable.
- After the traversal is complete, returned the final value of `jawab`.

My approach recursively traversed the binary search tree, identified leaf nodes and added their data to the sum. The final result is the sum of all leaf nodes in the given binary search tree.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n)$
  - $n$ : number of nodes in the tree
<!-- Add your time complexity here, e.g. $$O())$$ -->

- Space complexity : $O(n)$
  -  $O(n)$ in the worst case and $O(log n)$ in the average case for a balanced tree
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
   
## Code 

```
// User function Template for Java

/* Node class for the binary search tree 
class Node {
    int data;
    Node left, right;

    // Constructor to initialize a Node with a key
    Node(int key) {
        data = key;
        left = right = null;
    }
}
*/

class Solution {
    // Variable to store the sum of leaf nodes
    static int jawab;

    // Main function to calculate the sum of leaf nodes
    public static int sumOfLeafNodes(Node root) {
        // Resetting the answer variable before each function call
        jawab = 0;
        
        // Calling the helper function to traverse the tree and calculate the sum
        helper(root);
        
        // Returning the final sum of leaf nodes
        return jawab;
    }

    // Helper function to recursively traverse the tree and calculate the sum of leaf nodes
    static void helper(Node r) {
        // Base case: if the current node is null, return
        if (r == null) {
            return;
        }

        // Recursively calling the helper function for the left and right subtrees
        helper(r.left);
        helper(r.right);

        // If the current node is a leaf node, adding its data to the answer variable
        if (r.left == null && r.right == null) {
            jawab += r.data;
        }
    }
}
```
