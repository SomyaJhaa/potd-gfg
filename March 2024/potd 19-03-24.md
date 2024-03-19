## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 19-03-24 

## [Possible Paths in a Tree](https://www.geeksforgeeks.org/problems/possible-paths--141628/1)



## Intuition
The given code implements a solution to find the maximum weighted edge for each query in a disjoint set data structure (also known as union-find or merge-find data structure). The problem involves processing a series of weighted edges and answering queries based on a weight threshold.


## Approach

**Disjoint Set Initialization** :
- Initialized the parent and size arrays for the disjoint set.
- Each node is initially its own parent, and the size of each set is set to 1.

**Processing Weighted Edges** :
- Sorted the given edges based on their weights in ascending order.
- For each edge in the sorted list :
  - Finded the roots of the two nodes connected by the edge using the `findRoot` method.
  - If the roots are different, performed union of the two nodes using the `union` method.
  - Updated the `result` variable with the sum of squares of sizes of the merged sets.

**Stored Results** :
- Used a TreeMap to store the result for each weight threshold encountered during the processing of edges.
- For each query weight :
  - Finded the closest weight threshold less than or equal to the query weight using the `floorEntry` method of TreeMap.
  - If no such weight threshold exists, added 0 to the result list; otherwise, add the corresponding result to the list.

**Results** :
- Returned the list containing the results for each query.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $ O(n log n + q log n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ :  number of edges 

$q$ : number of queries
- Space complexity : $O( n )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Static variable to store the result
    static int result;

    // Method to find the root of a node in the disjoint set
    static int findRoot(int node, int[] parent) {
        
        // Path compression technique to find the root
        while (parent[node] != node) {
            parent[node] = parent[parent[node]]; // Path compression
            node = parent[node];
        }
        return node;
    }

    // Method to perform union of two nodes in the disjoint set
    static int union(int a, int b, int[] parent, int[] size) {
        // Finding the roots of the nodes
        int rootA = findRoot(a, parent);
        int rootB = findRoot(b, parent);
        
        // If both nodes are already in the same set, returning the square of their size
        if (rootA == rootB)
            return size[rootA] * size[rootA];
        
        // Union by rank to merge smaller set into larger set
        if (size[rootA] < size[rootB]) {
            int temp = rootA;
            rootA = rootB;
            rootB = temp;

            temp = a;
            a = b;
            b = temp;
        }

        // Updating result by adding the product of sizes of both sets
        result += size[rootA] * size[rootB];
        
        // Merging smaller set into larger set
        parent[rootB] = rootA;
        size[rootA] += size[rootB];

        return result;
    }

    // Method to find the maximum weighted edge for each query
    public static ArrayList<Integer> maximumWeight(int n, int[][] edges, int q, int[] queries) {
        
        // Initializing result to 0
        result = 0;

        // Arrays to store parent and size of each node in the disjoint set
        int[] parent = new int[n + 1];
        int[] size = new int[n + 1];

        // Initializing parent array with each node as its own parent and size array with 1
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1;
        }

        // List to store weighted edges
        ArrayList<int[]> weightedEdges = new ArrayList<>();
        for (int i = 0; i < n - 1; i++)
            weightedEdges.add(new int[]{edges[i][2], edges[i][0], edges[i][1]});
        weightedEdges.sort(Comparator.comparingInt(a -> a[0]));

        // TreeMap to store result for each weight threshold
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int i = 0; i < n - 1; i++) {
            int weight = weightedEdges.get(i)[0];
            int nodeA = weightedEdges.get(i)[1];
            int nodeB = weightedEdges.get(i)[2];
            map.put(weight, union(nodeA, nodeB, parent, size));
        }

        // ArrayList to store results for each query
        ArrayList<Integer> resultArray = new ArrayList<>();
        for (int i = 0; i < q; i++) {
            
            // Finding the closest weight threshold less than or equal to the query weight
            Map.Entry<Integer, Integer> entry = map.floorEntry(queries[i]);
            
            // If no such weight threshold exists, adding 0 to the result list
            if (entry == null)
                resultArray.add(0);
            // Otherwise, adding the result corresponding to the weight threshold to the result list
            else
                resultArray.add(entry.getValue());
        }

        return resultArray;
    }
}
```
