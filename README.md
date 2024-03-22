## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 22-03-24 

## [Diagonal sum in binary tree](https://www.geeksforgeeks.org/problems/diagonal-sum-in-binary-tree/1)

## Intuition
To calculate the diagonal sum of a binary tree, I traverse the tree in a diagonal manner, adding the values of nodes at the same diagonal level. I can implement this using a recursive approach.

## Approach

- I initialize an ArrayList to store the diagonal sums.
- Define a recursive function to calculate the diagonal sums.
- In each recursive call, update the diagonal sum at the corresponding index in the ArrayList.
- Traverse the tree recursively, moving to the right child and incrementing the diagonal level, and moving to the left child while keeping the diagonal level unchanged.
- Return the ArrayList containing the diagonal sums.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  number of nodes in the tree
- Space complexity : $O( h )$
$h$ : height of the tree
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

/*Complete the function below
Node is as follows:
class Node{
    int data;
    Node left,right;
    Node(int d){
        data=d;
        left=right=null;
    }
}
*/
class Tree {
    
    /**
     * Calculates the diagonal sum of the binary tree.
     * 
     * @param root The root node of the binary tree.
     * @return An ArrayList containing the diagonal sums.
     */
    public static ArrayList<Integer> diagonalSum(Node root) {
        
        // Initialize an ArrayList to store the diagonal sums
        ArrayList<Integer> diagonalSums = new ArrayList<>();
        
        // Call the recursive function to calculate diagonal sums
        calculateDiagonalSum(diagonalSums, root, 0);
        
        // Return the ArrayList containing diagonal sums
        return diagonalSums;
    }
    
    /**
     * Recursive function to calculate diagonal sums of the binary tree.
     * 
     * @param diagonalSums The ArrayList to store diagonal sums.
     * @param node The current node being processed.
     * @param level The current diagonal level.
     */
    private static void calculateDiagonalSum(ArrayList<Integer> diagonalSums, Node node, int level) {
        
        // If the ArrayList size matches the current diagonal level,
        // add the node's data to the sum, otherwise update the sum.
        if (diagonalSums.size() == level) {
            diagonalSums.add(node.data);
        } else {
            int sum = diagonalSums.get(level);
            sum += node.data;
            diagonalSums.set(level, sum);
        }
        
        // Recursively traverse the right child, maintaining the same level.
        if (node.right != null) {
            calculateDiagonalSum(diagonalSums, node.right, level);
        }
        
        // Recursively traverse the left child, incrementing the level.
        if (node.left != null) {
            calculateDiagonalSum(diagonalSums, node.left, level + 1);
        }
    }
}
```
