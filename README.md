#  Problem Of The Day Solutions GeeksForGeeks

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 08-02-24 
## [Check if all leaves are at same level](https://www.geeksforgeeks.org/problems/leaf-at-same-level/1)

## Intuition

This problem at hand involves determining whether a binary tree is balanced, where the subtrees of any node do not differ in depth by more than one level. Visually, a balanced tree exhibits an even structure without significant skewness.

## Approach

To assess the balance of a binary tree, I employed a recursive approach to calculate both the maximum and minimum depths of the tree. My fundamental idea was that, for a tree to be balanced, its maximum and minimum depths should coincide.

##### Base Case :
   - If the current node is `null`, the depth is considered 0.
   - For leaf nodes (nodes with no children), the depth is 1.

##### Founded Maximum Depth :
   - Recursively calculated the maximum depth of the left and right subtrees.
   - The maximum depth of the current node is the maximum value among the depths of its left and right subtrees, plus 1 for the current level.

##### Founded Minimum Depth :
   - Recursively calculated the minimum depth of the left and right subtrees.
   - For leaf nodes, returned 1.
   - The minimum depth of the current node is the minimum value among the depths of its left and right subtrees, plus 1 for the current level.

##### Checked Balanced Tree :
   - If the calculated maximum depth is equal to the minimum depth, the tree is considered balanced.
   - If the depths differ, the tree is not balanced.

##### Conclusion

My approach, through a comparison of maximum and minimum depths, offers a clear method to determine whether a binary tree meets the criteria of balance. The recursive nature of my solution facilitates a comprehensive exploration of the tree structure, enabling efficient depth comparisons.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(N)$
<!-- Add your time complexity here, e.g. $$O())$$ -->

$N$ : number of nodes in the tree.

- Space complexity : $O(N)$ 
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code 

```
//User function Template for Java

/* A Binary Tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}
*/

class Solution {

    // Checking if the tree is balanced
    boolean check(Node root) {
        // Finding the maximum and minimum depths
        int maxDepth = findMaxDepth(root);
        int minDepth = findMinDepth(root);

        // Returning true if the maximum and minimum depths are equal, indicating a balanced tree
        return maxDepth == minDepth;
    }

    // Helper method to find the maximum depth of the tree
    static int findMaxDepth(Node currentNode) {
        // Base case: if the current node is null, returniing 0
        if (currentNode == null)
            return 0;

        // Recursively finding the maximum depth of the left and right subtrees
        int leftDepth = findMaxDepth(currentNode.left);
        int rightDepth = findMaxDepth(currentNode.right);

        // Returning the maximum depth among the left and right subtrees, plus 1 for the current level
        return 1 + Math.max(leftDepth, rightDepth);
    }

    // Helper method to find the minimum depth of the tree
    static int findMinDepth(Node currentNode) {
        // Base case: if the current node is null, returning the maximum integer value
        if (currentNode == null)
            return Integer.MAX_VALUE;

        // Base case: if the current node is a leaf node, returning 1
        if (currentNode.left == null && currentNode.right == null)
            return 1;

        // Recursively finding the minimum depth of the left and right subtrees
        int leftDepth = findMinDepth(currentNode.left);
        int rightDepth = findMinDepth(currentNode.right);

        // Returning the minimum depth among the left and right subtrees, plus 1 for the current level
        return 1 + Math.min(leftDepth, rightDepth);
    }
}       
```
