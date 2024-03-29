## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 29-03-24 

## [Euler Circuit in an Undirected Graph](https://www.geeksforgeeks.org/problems/euler-circuit-in-a-directed-graph/1)

## Intuition
My given solution should check if an Eulerian circuit exists in a graph, using the following approach.

## Approach

**Initialization** :
   - Initialized a boolean array `ghumahua` to keep track of visited vertices during DFS traversal.

**Checked Connectivity** :
   - Called the `isConnected` method to check if the graph is connected. If not, returned false.

**Counted Odd-Degree Vertices** :
   - Iterated through all vertices and count the number of vertices with odd degree.

**Checked Eulerian Circuit Existence** :
   - If the count of odd-degree vertices is greater than 2, returned false.
   - If the count is exactly 0, returned true indicating the existence of an Eulerian circuit.

**DFS for Connectivity Check** :
   - Performed a DFS traversal starting from a vertex with non-zero degree.
   - Ensured that all non-zero degree vertices are visited during DFS traversal.

**Result** :
   - Returned true if the above conditions are satisfied; otherwise, return false.

My approach ensured that the graph is connected and then checks the number of vertices with odd degree to determine the existence of an Eulerian circuit.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(V + E)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$V$ : number of vertices

$E$ : number of edges
- Space complexity : $O(V)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Function to check if an Eulerian circuit exists in a graph
    public boolean isEularCircuitExist(int v, ArrayList<ArrayList<Integer>> adj) {
        
        // Array to keep track of visited vertices during DFS traversal
        boolean[] ghumahua = new boolean[v];
        
        // Checking if the graph is connected
        if (!isConnected(v, adj, ghumahua)){
            return false;
        }
        
        // Counting vertices with odd degree
        int visamDegree = 0;
        for (int i = 0; i < v; i++) {
            if (adj.get(i).size() % 2 != 0){
                visamDegree++;
            }
        }
        
        // If more than 2 vertices have odd degree, graph doesn't have an Eulerian circuit
        if (visamDegree > 2){
            return false;
        }
        
        // If exactly 0 vertices have odd degree, graph has an Eulerian circuit
        return visamDegree == 0;
    }

    // Function to check if the graph is connected
    private boolean isConnected(int v, ArrayList<ArrayList<Integer>> adj, boolean[] visited) {
        // Initializing the visited array
        for (int i = 0; i < v; i++) {
            visited[i] = false;
        }
        
        // Finding a vertex with non-zero degree
        int i;
        for (i = 0; i < v; i++) {
            if (adj.get(i).size() != 0) {
                break;
            }
        }
        
        // If there are no edges in the graph, returning true
        if (i == v){
            return true;
        }
        
        // Performing DFS traversal starting from a vertex with non-zero degree
        dfsHelper(i, adj, visited);
        
        // Checking if all non-zero degree vertices are visited
        for (i = 0; i < v; i++) {
            if (!visited[i] && adj.get(i).size() > 0) {
                return false;
            }
        }
        
        return true;
    }
    
    // Depth First Search Helper Function
    private void dfsHelper(int v, ArrayList<ArrayList<Integer>> adj, boolean[] visited) {
        // Marking the current vertex as visited
        visited[v] = true;
        
        // Recur for all vertices adjacent to the current vertex
        Iterator<Integer> i = adj.get(v).listIterator();
        while (i.hasNext()) {
            int n = i.next();
            if (!visited[n]) {
                dfsHelper(n, adj, visited);
            }
        }
    }
}   
```
