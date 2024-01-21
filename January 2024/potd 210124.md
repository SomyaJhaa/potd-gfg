#  Problem Of The Day Solutions GeeksForGeeks

## Today's 21-01-24 
## [Vertex Cover](https://www.geeksforgeeks.org/problems/vertex-cover/1)

## Intuition
A vertex cover of a graph is a set of vertices such that every edge in the graph is incident to at least one vertex from the set. This problem is to find the smallest possible size of such a vertex cover.

## Approach

#### Initialization
- I represented the graph using a 2D boolean array called `adjacencyMatrix`. `adjacencyMatrix[i][j]` is true if there is an edge between vertex `i` and vertex `j`.
- The function `addEdge` is used to fill the adjacency matrix based on the given edges.

#### Finding Minimum Vertex Cover Size
**Function `vertexCover`**
- It takes the number of nodes `n`, the number of edges `m`, and a 2D array `edges` representing the edges between nodes.
- Initializes and fills the adjacency matrix using the `addEdge` function.
- Calls the `findMinimumCoverSize` function to find the minimum size of the vertex cover.

**Function `findMinimumCoverSize`**
- It uses binary search to find the minimum size of the vertex cover.
- Calls the `isVertexCover` function to check if a vertex cover of a certain size is valid.
- The result is the minimum size of the vertex cover.

**Function `isVertexCover`**
- Checks whether a vertex cover of a given size covers all the edges in the graph.
- Utilizes bitmasking to represent the selected vertices.
- Iterates through all possible combinations of vertices to find a valid cover.
- Uses a 2D array `visited` to keep track of visited edges during the checking process.

**Function `initializeVisited`**
- Initializes a 2D array `visited` to keep track of visited edges during the checking process.

### Summary
My code employs an adjacency matrix, bitmasking, and binary search to efficiently find the minimum size of a vertex cover for the given graph. My approach involves checking the validity of vertex covers of different sizes until the minimum valid size is found.

---
Have a look at the code , still have any confusion then please let me know in the comments
Keep Solving.:)

## Complexity
- Time complexity : $O(log n * 2^n)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of nodese

- Space complexity : $O(max^2)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$max = MAX NODES$ : 30 ( I used )

## Code C++
```
// User function Template for C++

#define MAXN 25

class Solution{
public:
    // Adjacency matrix for the graph
    bool adjacencyMatrix[MAXN][MAXN];
    
    int vertexCover(int n, std::vector<std::pair<int, int>> &edges) {
        // Initialize the adjacency matrix
        memset(adjacencyMatrix, 0, sizeof adjacencyMatrix);

        // Add edges to the graph
        for (auto edge : edges) {
            addEdge(edge.first, edge.second);
        }

        // Find the minimum size of a vertex cover
        return findMinCoverSize(n, edges.size());
    }

    // Function to check if a vertex cover of size k exists
    bool isVertexCover(int numVertices, int k, int numEdges) {
        int setBits = (1 << k) - 1;
        int upperBound = (1 << numVertices);
        bool visited[MAXN][MAXN];

        while (setBits < upperBound) {
            // Initialize visited array
            memset(visited, 0, sizeof visited);
            int edgeCount = 0;

            // Iterate over vertices and check if they are part of the current vertex cover
            for (int vertexBit = 1, vertex = 1; vertexBit < upperBound; vertexBit = vertexBit << 1, vertex++) {
                if (setBits & vertexBit) {
                    // Check neighbors of the current vertex
                    for (int neighbor = 1; neighbor <= numVertices; neighbor++) {
                        if (adjacencyMatrix[vertex][neighbor] && !visited[vertex][neighbor]) {
                            visited[vertex][neighbor] = 1;
                            visited[neighbor][vertex] = 1;
                            edgeCount++;
                        }
                    }
                }
            }

            // If the edge count matches the total number of edges, a valid cover is found
            if (edgeCount == numEdges)
                return true;

            // Update the set of selected vertices using bitwise operations
            int rightmostSetBit = setBits & -setBits;
            int newSet = setBits + rightmostSetBit;
            setBits = (((newSet ^ setBits) >> 2) / rightmostSetBit) | newSet;
        }

        // No valid vertex cover of size k found
        return false;
    }

    // Function to find the minimum size of a vertex cover using binary search
    int findMinCoverSize(int numVertices, int numEdges) {
        int left = 1, right = numVertices;

        while (right > left) {
            int mid = (left + right) >> 1;

            // Check if a vertex cover of size mid exists
            if (isVertexCover(numVertices, mid, numEdges) == false)
                left = mid + 1;
            else
                right = mid;
        }

        // Return the minimum size of a vertex cover
        return left;
    }

    // Function to add an undirected edge to the graph
    void addEdge(int u, int v) {
        adjacencyMatrix[u][v] = 1;
        adjacencyMatrix[v][u] = 1;
    }
    
};
```

## Code Java
```
//User function Template for Java

class Solution {
    
    static final int MAX_NODES = 30;
    static boolean[][] adjacencyMatrix = new boolean[MAX_NODES][MAX_NODES];

    public int vertexCover(int n, int m, int[][] edges) {
        // Initializing the adjacency matrix with the given edges
        initializeAdjacencyMatrix();

        for (int[] edge : edges) {
            addEdge(edge[0], edge[1]);
        }

        // Find the minimum vertex cover size
        return findMinimumCoverSize(n, edges.length);
    }

    // Initializing the adjacency matrix with all false values
    static void initializeAdjacencyMatrix() {
        for (int i = 0; i < MAX_NODES; i++) {
            Arrays.fill(adjacencyMatrix[i], false);
        }
    }

    // Checking if the current vertex cover size is valid
    static boolean isVertexCover(int numNodes, int coverSize, int numEdges) {
        int currentCover = (1 << coverSize) - 1;
        int bound = (1 << numNodes);
        boolean[][] visited = new boolean[MAX_NODES][MAX_NODES];

        while (currentCover < bound) {
            initializeVisited(visited);
            int coveredEdges = 0;

            for (int currentNode = 1, vertex = 1; currentNode < bound; currentNode = currentNode << 1, vertex++) {
                if ((currentCover & currentNode) != 0) {
                    for (int connectedNode = 1; connectedNode <= numNodes; connectedNode++) {
                        if (adjacencyMatrix[vertex][connectedNode] && !visited[vertex][connectedNode]) {
                            visited[vertex][connectedNode] = true;
                            visited[connectedNode][vertex] = true;
                            coveredEdges++;
                        }
                    }
                }
            }

            if (coveredEdges == numEdges) {
                return true; // The current cover size is valid
            }

            int x = currentCover & -currentCover;
            int r = currentCover + x;
            currentCover = (((r ^ currentCover) >> 2) / x) | r;
        }

        return false; // The current cover size is not valid
    }

    // Initializing the visited array with all false values
    static void initializeVisited(boolean[][] visited) {
        for (int i = 0; i < MAX_NODES; i++) {
            Arrays.fill(visited[i], false);
        }
    }

    // Finding the minimum vertex cover size using binary search
    static int findMinimumCoverSize(int numNodes, int numEdges) {
        int left = 1, right = numNodes;

        while (right > left) {
            int mid = (left + right) >> 1;

            if (!isVertexCover(numNodes, mid, numEdges)) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        return left; // Return the minimum cover size
    }

    // Adding an edge to the adjacency matrix
    static void addEdge(int startNode, int endNode) {
        adjacencyMatrix[startNode][endNode] = true;
        adjacencyMatrix[endNode][startNode] = true;
    }
}

```

