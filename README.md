## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 21-03-24 

## [ZigZag Tree Traversal](https://www.geeksforgeeks.org/problems/zigzag-tree-traversal/1)

## Intuition
The task is to perform a zigzag traversal of a binary tree, alternating between left-to-right and right-to-left at each level.

## Approach

- I created a function named `zigZagTraversal` that takes the root node of the binary tree as input and returns the zigzag traversal result as an ArrayList.
- Initialize an ArrayList named `jawab` to store the zigzag traversal result.
- Return an empty list if the root node is null, as there are no nodes to traverse.
- Create a Queue named `q` to perform level order traversal of the binary tree.
- Add the root node to the queue.
- Initialize a boolean variable `leftToRight` to true, indicating the direction of traversal.
- Iterate until the queue is empty :
  - Get the size of the queue to determine the number of nodes at the current level.
  - Create an ArrayList named `levelNodes` to store the nodes at the current level.
  - Iterate over the nodes at the current level :
    - Poll the node from the front of the queue.
    - If the left child of the current node exists, add it to the queue.
    - If the right child of the current node exists, add it to the queue.
    - Add the value of the current node to the `levelNodes` list.
  - If the traversal direction is from right to left, reverse the `levelNodes` list.
  - Add all the nodes in the `levelNodes` list to the `jawab` list.
  - Toggle the direction of traversal for the next level by negating the value of `leftToRight`.
- Return the `jawab` list containing the zigzag traversal of the binary tree.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  number of nodes in the binary tree
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java


/*class Node
{
    int data;
    Node left,right;
    Node(int d)
    {
        data=d;
        left=right=null;
    }
}*/

class GFG {
    
    // Function to perform zigzag traversal of a binary tree
    ArrayList<Integer> zigZagTraversal(Node rootNode) {
        
        // List to store the zigzag traversal result
        ArrayList<Integer> jawab = new ArrayList<>();
        
        // Returning empty list if the root node is null
        if (rootNode == null){
            return jawab;
        }
        
        // Queue to perform level order traversal
        Queue<Node> q = new LinkedList<>();
        q.add(rootNode);
        
        // Flag to track the direction of traversal
        boolean leftToRight = true;
        
        // Looping until the q is empty
        while (!q.isEmpty()) {
            int size = q.size();
            ArrayList<Integer> levelNodes = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Node current = q.poll();
                if (current.left != null){
                    q.add(current.left);
                }
                if (current.right != null){
                    q.add(current.right);
                }
                levelNodes.add(current.data);
            }
            
            // Reversing the level nodes if traversing from right to left
            if (!leftToRight) {
                Collections.reverse(levelNodes);
            }
            
            // Adding the level nodes to the result list
            jawab.addAll(levelNodes);
            
            // Toggling the direction for the next level
            leftToRight = !(leftToRight);
        }
        
        // Returning the zigzag traversal result
        return jawab;
    }
}
```
