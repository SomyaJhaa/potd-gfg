## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 03-04-24 

## [Kth common ancestor in BST](https://www.geeksforgeeks.org/problems/kth-common-ancestor-in-bst/1)

## Intuition
-  Given a Binary Search Tree (BST) with n (n >= 2) nodes, I aim to find the kth common ancestor of nodes x and y.
- The common ancestor of two nodes x and y is a node that is an ancestor of both x and y.
- To find the kth common ancestor, I first find the Lowest Common Ancestor (LCA) of nodes x and y in the BST.
- Then, I traverse the path from the LCA to the root and identify the kth node in this path.

## Approach
- Finded the Lowest Common Ancestor (LCA) of nodes x and y in the BST.
   - Start from the root node.
   - If both x and y are less than the current node's value, move to the left subtree.
   - If both x and y are greater than the current node's value, move to the right subtree.
   - If x and y are on different sides of the current node's value, the current node is the LCA.
- Finded the path from the root to the LCA.
   - Started from the root and traverse towards the LCA.
   - While traversing, keep track of the nodes visited in an ArrayList.
- Reversed the path ArrayList to traverse from the LCA towards the root.
- Returned the kth element in the reversed path ArrayList as the kth common ancestor.
   - If the path length is less than k, return -1 as the kth ancestor does not exist.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(h)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$h$ : height of the binary tree

- Space complexity : $O(h)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Function to find the kth common ancestor of nodes x and y
    public int kthCommonAncestor(Node root, int k, int x, int y) {
        
        // Finding the Lowest Common Ancestor (LCA) of nodes x and y
        Node lca = findLowestCommonAncestor(root, x, y);
        
        // ArrayList to store the path from the root to the LCA
        ArrayList<Integer> path = new ArrayList<>();
        
        // Finding the path from the root to the LCA
        findPathToNode(root, lca, path);
        
        // Reversing the path array to traverse from the LCA towards the root
        Collections.reverse(path);

        // If the path length is less than k, kth ancestor does not exist
        if (path.size() < k) return -1;

        // Returning the kth ancestor from the reversed path array
        return path.get(k - 1);
    }
    
    
    // Function to find the Lowest Common Ancestor (LCA) of nodes x and y
    Node findLowestCommonAncestor(Node root, int x, int y) {
        if (root == null) return null;

        // If both x and y are less than the current node's value, then the LCA lies in the left subtree
        if (x < root.data && y < root.data) return findLowestCommonAncestor(root.left, x, y);

        // If both x and y are greater than the current node's value, then the LCA lies in the right subtree
        if (x > root.data && y > root.data) return findLowestCommonAncestor(root.right, x, y);

        // If x and y are on different sides of the current node's value, then the current node is the LCA
        return root;
    }

    // Function to find the path from the root to a specific node
    void findPathToNode(Node root, Node node, ArrayList<Integer> path) {
        path.add(root.data);
        
        // If the current node's value matches the target node's value, we have found the path
        if (root.data == node.data){
            return;
        }
        // If the target node's value is greater than the current node's value, continue searching in the right subtree
        else if (node.data > root.data){
            findPathToNode(root.right, node, path);
        }
        // If the target node's value is less than the current node's value, continue searching in the left subtree
        else{
            findPathToNode(root.left, node, path);
        }
    }

}
```
