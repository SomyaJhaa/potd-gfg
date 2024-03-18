## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 18-03-24 

## [Level order traversal](https://www.geeksforgeeks.org/problems/level-order-traversal/1)

## Intuition
- Perform a level order traversal of the binary tree.
- Use a queue to keep track of nodes at each level.
- Iterate through each level and add the nodes' values to the result list.

## Approach

**Initialization :** Initialized an empty ArrayList to store the level order traversal.

**Base Case :** If the root is null, returned an empty ArrayList.

**Breadth-First Traversal :** Used a queue to perform a breadth-first traversal of the tree.

**Iterated Levels :** While the queue is not empty, iterated through each level :
- For each node in the current level :
  - Added its value to the result list.      
  - If the left child exists, enqueued it.
  - If the right child exists, enqueued it.

**Result :** Returned the ArrayList containing the level order traversal.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  number of nodes in the tree
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

/*
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
class Solution
{
    //Function to return the level order traversal of a tree.
    static ArrayList <Integer> levelOrder(Node root) 
    {
        // Your code here
        if( root == null){
            return new ArrayList<>();
        }
        ArrayList<Integer> jawab = new ArrayList<>();              // to store the jawabwer : initially added root node
        Queue<Node> q = new ArrayDeque<>( Arrays.asList(root));  // maintaining queue to store nodes as they appear left to right in a level: 

        while( !q.isEmpty()){
            for( int i = q.size(); i > 0; i--){         // iterating over each element in that level
                Node t = q.poll();                      // popping queue to get a node
                jawab.add(t.data);                        // storing its value
                if( t.left != null){                    // if left child present then adding it to queue to furthur iterations in upcoming levels
                    q.offer(t.left);
                }
                if( t.right != null){                   // if right child present then adding it to queue to furthur iterations in upcoming levels
                    q.offer(t.right);
                }
            }
        }
        return jawab;
    }
}
```
