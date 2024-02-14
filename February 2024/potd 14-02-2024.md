## Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 14-02-24 
## [Find all Critical Connections in the Graph](https://www.geeksforgeeks.org/problems/critical-connections/1)


**Intuition:**

The given code implements the Tarjan's algorithm for finding critical connections in an undirected graph. The algorithm uses depth-first search (DFS) to find bridges (critical connections) in the graph. A bridge is an edge whose removal increases the number of connected components in the graph.

**Approach:**

1. The DFS function is implemented to traverse the graph and identify the critical connections.
2. The `visited` array keeps track of whether a node has been visited during the DFS traversal.
3. The `lo` and `hi` arrays are used to store the lowest and highest visited time for each node in the DFS traversal.
4. The `time` variable is incremented with each new node visited, representing the timestamp of the traversal.
5. During the DFS traversal, if a back edge is encountered (i.e., an edge to an already visited node that is not the parent), the `lo` value of the current node is updated with the minimum `lo` value of the destination node.
6. If `hi` value of the current node is less than `lo` value of the destination node, it indicates a bridge. The edge is added to the `ans` vector after sorting the nodes in ascending order.
7. The `ans` vector contains all critical connections in sorted order.

**Time Complexity:**

The time complexity of the DFS traversal is O(v + e), where v is the number of vertices and e is the number of edges. Sorting the `ans` vector at the end takes O(e * log(e)) time. Therefore, the overall time complexity is O(v + e + e * log(e)), which can be simplified to O(v + e * log(e)).

**Space Complexity:**

The space complexity is O(v), where v is the number of vertices. The `visited`, `lo`, and `hi` arrays each require O(v) space. Additionally, the `ans` vector stores the critical connections, which can be at most O(e) in the worst case.

Overall, the space complexity is O(v).


## Code 

```
class Solution {
 public:
 
    int time =1;
      void dfs(vector<int> adj[],vector<int>&visited,vector<int>&lo,vector<int> &hi,int curr,int parent, vector<vector<int>> &ans){
          
          visited[curr]=1;
          lo[curr]= hi[curr]= time;
          time++;
          
          for(auto it: adj[curr]){
              
              if(it==parent) continue;
              if(visited[it]==0){
                  
                  dfs(adj,visited,lo,hi,it,curr,ans);
                        lo[curr]= min(lo[curr],lo[it]);
                  if(hi[curr]< lo[it]){
                      vector<int> temp{curr,it};
                      
                      sort(temp.begin(),temp.end());
                      ans.push_back(temp);
                  }
              }
              else{
                  lo[curr]= min(lo[curr],lo[it]);
              }
          }
      }
	vector<vector<int>>criticalConnections(int V, vector<int> adj[]){
	    vector<int>visited(V,0);
	    vector<int> lo(V);
	    vector<int> hi(V);
	    vector<vector<int>> ans;
	    dfs(adj,visited,lo,hi,0,-1,ans);
	  sort(ans.begin(),ans.end());
	    return ans;
	    
	}
};
    
```
