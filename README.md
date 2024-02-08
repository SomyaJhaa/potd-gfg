#  Problem Of The Day Solutions GeeksForGeeks

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 08-02-24 
<<<<<<< HEAD
## [Check if all leaves are at same level
](https://www.geeksforgeeks.org/problems/leaf-at-same-level/1)
=======
## [Check if all leaves are at same level](https://www.geeksforgeeks.org/problems/leaf-at-same-level/1)
>>>>>>> 67bcbe6934ca9238f769ccf51c8477f95e63576b

**Intuition:**
To check if all leaf nodes in a binary tree are at the same level, we can perform a level-order traversal using a queue. During the traversal, we keep track of the level of each node. If we encounter a leaf node, we compare its level with the level of the previous leaf nodes. If the levels are consistent, we continue; otherwise, we return false.

<<<<<<< HEAD
**Approach:**
1. Initialize a queue to perform a level-order traversal.
2. Enqueue the root node along with its level (starting from 0).
3. Use a variable `prev` to keep track of the level of the previous leaf nodes. Initialize it to -1.
4. While the queue is not empty, dequeue a node and check if it is a leaf node.
5. If it is a leaf node, compare its level with the previous leaf nodes' level (`prev`).
6. If `prev` is -1, update it with the current leaf node's level.
7. If `prev` is not -1 and is different from the current leaf node's level, return false.
8. Enqueue the left and right children of the current node if they exist, along with their levels (level + 1).
9. If the traversal completes without returning false, all leaf nodes are at the same level, so return true.
=======
This problem at hand involves determining whether a binary tree is balanced, where the subtrees of any node do not differ in depth by more than one level. Visually, a balanced tree exhibits an even structure without significant skewness.
>>>>>>> 67bcbe6934ca9238f769ccf51c8477f95e63576b

**Time Complexity:**
The time complexity is O(n), where n is the number of nodes in the binary tree. We visit each node once during the level-order traversal.

<<<<<<< HEAD
**Space Complexity:**
The space complexity is O(height of the tree), where the height is the maximum number of levels in the tree. In the worst case, the queue may contain all nodes at the last level, leading to a space complexity of O(2^(h-1)), where h is the height of the tree.

=======
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
>>>>>>> 67bcbe6934ca9238f769ccf51c8477f95e63576b

## Code 

```
//User function Template for Java

<<<<<<< HEAD
class Solution{
  public:
    /*You are required to complete this method*/
    bool check(Node *root)
    {
        if(!root)
        return true;
        queue<pair<Node*,int>>q;
        q.push({root,0});
        int prev = -1;
        while(!q.empty())
        {
            int size = q.size();
            int lev = q.front().second;
            for(int i=0;i<size;i++)
            {
                Node* temp = q.front().first;
                q.pop();
                if(!temp->left && !temp->right)
                {
                    if(prev == -1)
                    prev = lev;
                    else if(prev!=lev)
                    return false;
                }
                if(temp->left)
                {
                    q.push({temp->left,lev+1});
                }
                if(temp->right)
                {
                    q.push({temp->right,lev+1});
                }
            }
        }
        return true;
    }
};

=======
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
>>>>>>> 67bcbe6934ca9238f769ccf51c8477f95e63576b
```
