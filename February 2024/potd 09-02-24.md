#  Problem Of The Day Solutions GeeksForGeeks

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 09-02-24 
## [Check for Children Sum Property in a Binary Tree](https://www.geeksforgeeks.org/problems/children-sum-parent/1)

## Intuition

This problem at hand involved verifying whether every node in a tree adheres to a sum property: having a value equal to the sum of its child nodes. My algorithm employed a level-order traversal to systematically process nodes and validate this sum property across the entire tree.

## Approach

**Checked for Empty Tree :**
- If the tree is empty, it trivially satisfies the sum property.

**Initialized a Queue for Level Order Traversal :**
- Established a queue tailored for a level-order traversal.

**Level Order Traversal :**
- Employed a while loop until the queue becomes empty.
- Dequeued the current node and process its children.

**Calculated Sum and Checked Property :**
- For each node, calculated the sum of its child nodes and ensured it equals the node's value.
- Returned false if the sum property is violated.

**Returned the Result :**
- If the entire tree satisfied the sum property, returned true.

My algorithm systematically verified the sum property for each node in a tree using a level-order traversal, ensuring the property holds true across the entire tree.

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


/*Complete the function below
Node is as follows:
class Node{
	int data;
	Node left,right;
	
	Node(int key)
	{
	    data = key;
	    left = right = null;
	}
}

*/

class Solution {
    // Function to check whether all nodes of a tree have the value 
    // equal to the sum of their child nodes.
    
    public static int isSumProperty(Node root) {
        if (root == null) {
            // Handling the case where the tree is empty
            return 1;  // As an empty tree vacuously satisfies the sum property
        }
        return Helper(root) ? 1 : 0;
    }

    static Queue<Node> q;

    static boolean Helper(Node root) {
        // Initializing a queue for level order traversal
        q = new LinkedList<>();
        // Enqueuing the root node to start the traversal
        q.offer(root);
        // Enqueuing null to mark the end of the current level
        q.offer(null);

        while (!q.isEmpty()) {
            // Dequeuing the current node
            Node tatkal = q.poll();

            // If the current node is null, it indicates the end of the current level
            if (tatkal == null) {
                // If there are more elements in the tree, enqueuing null to mark the end of the next level
                if (!q.isEmpty()) {
                    q.offer(null);
                    continue;
                }
            } else {
                // Initializing the sum of child node values
                int jor = 0;
                
                // Enqueuing the left child and update the sum
                if (tatkal.left != null) {
                    q.offer(tatkal.left);
                    jor += tatkal.left.data;
                }
                
                // Enqueuing the right child and update the sum
                if (tatkal.right != null) {
                    q.offer(tatkal.right);
                    jor += tatkal.right.data;
                }
                
                // Checking if the sum of child node values is not equal to the current node's data
                // Also, ensuring that the sum is not zero (to handle leaf nodes)
                if (jor != tatkal.data && jor != 0) {
                    return false;  // Returning false if the sum property is violated
                }
            }
        }
        // Returning true if the entire tree satisfies the sum property
        return true;
    }
}    
```
