#  Problem Of The Day Solutions GeeksForGeeks

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 08-02-24 
## [Check if all leaves are at same level
](https://www.geeksforgeeks.org/problems/leaf-at-same-level/1)

**Intuition:**
To check if all leaf nodes in a binary tree are at the same level, we can perform a level-order traversal using a queue. During the traversal, we keep track of the level of each node. If we encounter a leaf node, we compare its level with the level of the previous leaf nodes. If the levels are consistent, we continue; otherwise, we return false.

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

**Time Complexity:**
The time complexity is O(n), where n is the number of nodes in the binary tree. We visit each node once during the level-order traversal.

**Space Complexity:**
The space complexity is O(height of the tree), where the height is the maximum number of levels in the tree. In the worst case, the queue may contain all nodes at the last level, leading to a space complexity of O(2^(h-1)), where h is the height of the tree.


## Code 

```

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

```
