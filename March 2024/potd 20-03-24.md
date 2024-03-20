## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 20-03-24 

## [Sum of nodes on the longest path from root to leaf node](https://www.geeksforgeeks.org/problems/sum-of-the-longest-bloodline-of-a-tree/1)

## Intuition
The task is to find the sum of the longest path from the root to a leaf node in a binary tree. We can achieve this by recursively traversing the tree and keeping track of the maximum height and sum of the longest path found so far.

## Approach

1. I defined a class named PathSumCalculator.
2. Inside the class, define two instance variables: maxHeight and longestPathSum, to keep track of the maximum height and sum of the longest path found so far.
3. Define a recursive method named calculateLongestRootToLeafPathSum, which takes three parameters: currentNode (the current node being processed), currentHeight (the height of the current node), and currentSum (the sum of the path from the root to the current node).
4. In the calculateLongestRootToLeafPathSum method:
   - Check if the currentNode is null. If so, return.
   - If the currentNode is a leaf node (both left and right children are null):
     - Calculate the sum of the path from the root to this leaf node by adding the currentNode's data to the currentSum.
     - Update maxHeight and longestPathSum if the current path is longer than the previously found longest path.
   - Recursively call the method for the left and right children of the currentNode, updating the height and sum accordingly.
5. Define a method named findLongestRootToLeafPathSum, which takes the rootNode as a parameter.
6. Inside findLongestRootToLeafPathSum:
   - Initialize maxHeight and longestPathSum to zero.
   - Call the calculateLongestRootToLeafPathSum method with the rootNode, starting height (0), and starting sum (0).
   - Return the longestPathSum, which holds the sum of the longest path from the root to a leaf node in the binary tree.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( n )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  number of nodes 
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

/*
node class of binary tree
class Node {
    int data;
    Node left, right;
    
    public Node(int data){
        this.data = data;
    }
}
*/
class Solution{
    public int sumOfLongRootToLeafPath(Node root) {
        maxHeight = longestPathSum = 0;
        // Call the recursive method to calculate the longest path sum 
        calculateLongestRootToLeafPathSum(root, 0, 0);
        return longestPathSum;
    }

    int maxHeight, longestPathSum;
    
    // Define a method named calculateLongestRootToLeafPathSum
    void calculateLongestRootToLeafPathSum(Node currentNode, int currentHeight, int currentSum) {
        // Base case: If the current node is null, return 
        if (currentNode == null)
            return;
        
        // If the current node is a leaf node, calculate the sum of the path from the root to this leaf node
        if (currentNode.left == null && currentNode.right == null) {
            currentSum += currentNode.data;
            
            // Update maxHeight and longestPathSum if the current path is longer than the previously found longest path
            if (currentHeight > maxHeight) {
                maxHeight = currentHeight;
                longestPathSum = currentSum;
            } else if (currentHeight == maxHeight) {
                longestPathSum = Math.max(longestPathSum, currentSum);
            }
                
            return;
        }
        
        // Recursively call the method for the left and right children of the current node 
        currentSum += currentNode.data;
        calculateLongestRootToLeafPathSum(currentNode.left, currentHeight + 1, currentSum);
        calculateLongestRootToLeafPathSum(currentNode.right, currentHeight + 1, currentSum);
    }
    
}
```
