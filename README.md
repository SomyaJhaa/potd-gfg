## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 30-03-24 

## [Minimum element in BST](https://www.geeksforgeeks.org/problems/minimum-element-in-bst/1)

## Intuition
In a Binary Search Tree (BST), the minimum valued element is always located at the leftmost node. Therefore, to find the minimum element, I need to traverse the BST towards the left child recursively until I reach a node with no left child. That node will contain the minimum value in the BST.

## Approach

- I started at the root node.
- While the left child of the current node is not null, moved to the left child.
- Returned the value of the current node when there are no more left children.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(h)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$h$ : height of the tree

In the worst-case scenario, the tree is skewed, and the height h is equal to the number of nodes in the tree. Therefore, the time complexity is $O(N)$, where N is the number of nodes in the tree
- Space complexity : $O(1)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

/*
class Node {
    int data;
    Node left;
    Node right;
    Node(int data) {
        this.data = data;
        left = null;
        right = null;
    }
}
*/
class Solution {
    // Function to find the minimum element in the given BST.
    int minValue(Node root) {
        // code here
        
        // Base case: if root is null, return -1 or throw an error indicating that the tree is empty.
        if (root == null) {
            return -1;
        }
        
        // Traverse towards the leftmost node
        while (root.left != null) {
            root = root.left;
        }
        
        // Return the value of the leftmost node
        return root.data;
    }
}   
```
