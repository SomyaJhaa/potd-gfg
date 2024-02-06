## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 07-02-24 
## [Min distance between two given nodes of a Binary Tree](https://www.geeksforgeeks.org/problems/min-distance-between-two-given-nodes-of-a-binary-tree/1)

## Intuition

The task is to find the distance between two nodes (`a` and `b`) in a binary tree. The distance is defined as the number of edges on the path from one node to the other. To solve this problem efficiently, I employed a Depth-First Search (DFS) approach.

## Approach

**DFS Traversal :**
   - Utilized a recursive DFS traversal to explore the binary tree.
   - Kept track of the distance between the current node and the target nodes `a` and `b` in the left and right subtrees.

**Updated Distance (`jawab`):**
   - If the current node is one of the target nodes (`a` or `b`), updated the `jawab` variable based on the distances obtained from the left and right subtrees.
   - Handled the cases where both target nodes are found, only one target node is found, or neither target node is found.

**Returned the Result :**
   - The final result is stored in the `jawab` variable, which represents the distance between the two target nodes in the binary tree.

My approach ensured an efficient exploration of the binary tree, updating the distance as soon as both target nodes are found. My recursive DFS traversal allowed for a systematic examination of the tree, and the `jawab` variable was updated based on the conditions encountered during traversal.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(N)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

$N$ : number of nodes in the binary tree.

- Space complexity : $O(H)$ 
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$H$ : height of the tree.

## Code 

```

// FUNCTION CODE
/* A Binary Tree node
class Node
{
    int data;
    Node left, right;
   Node(int item)    {
        data = item;
        left = right = null;
    }
} */

/* Should return minimum distance between a and b
   in a tree with given root*/
class GfG {
    
    static int jawab;

    // Function to find the distance between two nodes in a binary tree
    int findDist(Node root, int a, int b) {
        // Your code here
        jawab = 0;
        helper(root, a, b);
        return jawab;
    }

    // Helper function for DFS traversal to find the distance between two nodes
    static int helper(Node root, int a, int b) {
        if (root == null) {
            return 0;
        }

        // Recursive calls for left and right subtrees
        int l = helper(root.left, a, b);
        int r = helper(root.right, a, b);

        // Checking if the current node is one of the target nodes
        if (root.data == a || root.data == b) {
            // If one of the target nodes is found, then updating jawab based on left and right distances
            if (l != 0 || r != 0) {
                jawab = Math.max(l, r);
                return 0;
            } else {
                // If the current node is a target node with no valid distance found, then returning 1
                return 1;
            }
        } else if (l != 0 && r != 0) {
            // If both target nodes are found in left and right subtrees, then updating jawab accordingly
            jawab = l + r;
            return 0;
        } else if (l != 0 || r != 0) {
            // If one target node is found, then returning the maximum distance from either subtree plus 1
            return Math.max(l, r) + 1;
        }

        // Default case, returning 0
        return 0;
    }
}
```
