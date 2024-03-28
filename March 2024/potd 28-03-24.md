## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 28-03-24 

## [City With the Smallest Number of Neighbors at a Threshold Distance](https://www.geeksforgeeks.org/problems/city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/1)

## Intuition
My algorithm should aim to find the city that minimizes the number of reachable cities within a given distance threshold. It accomplishes this by using the Floyd-Warshall algorithm to compute all shortest paths between cities, then iterates through each city to count the number of reachable cities within the threshold.

## Approach

**Initialization** :
   - Initialized an adjacency matrix to represent distances between cities, setting all distances to infinity except self-distances, which are set to 0.

**Populated Adjacency Matrix** :
   - Populated the adjacency matrix with distances from the given edges.

**Floyd-Warshall Algorithm** :
   - Applied the Floyd-Warshall algorithm to compute all shortest paths between cities.

**Finded Optimal City** :
   - Iterated through each city and count the number of reachable cities within the distance threshold.
   - Updated the optimal city if a city with fewer reachable cities is found.

**Result** :
   - Returned the index of the optimal city found.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(numOfCities^3)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
- Space complexity : $O(numOfCities^2)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Method to find the city with the minimum number of reachable cities within the distance threshold
    public int findCity(int numOfCities, int numOfEdges, int[][] edges, int distanceThreshold) {
      
        // Initializing the adjacency matrix to represent distances between cities
        int[][] adjacencyMatrix = new int[numOfCities][numOfCities];
        
        // Initializing all distances to infinity (Integer.MAX_VALUE/2 to avoid overflow) and set distances to self as 0
        for (int[] row : adjacencyMatrix) {
            Arrays.fill(row, Integer.MAX_VALUE / 2);
        }
        for (int i = 0; i < numOfCities; i++) {
            adjacencyMatrix[i][i] = 0;
        }
        
        // Populating the adjacency matrix with distances from given edges
        for (int[] edge : edges) {
            int city1 = edge[0];
            int city2 = edge[1];
            int distance = edge[2];
            adjacencyMatrix[city1][city2] = adjacencyMatrix[city2][city1] = distance;
        }
        
        // Applying Floyd-Warshall algorithm to find all shortest paths
        for (int k = 0; k < numOfCities; k++) {
            for (int i = 0; i < numOfCities; i++) {
                for (int j = 0; j < numOfCities; j++) {
                    adjacencyMatrix[i][j] = Math.min(adjacencyMatrix[i][j], adjacencyMatrix[i][k] + adjacencyMatrix[k][j]);
                }
            }
        }
        
        // Finding the city with the minimum number of reachable cities within the distance threshold
        int minReachableCities = numOfCities + 1;
        int optimalCity = -1;
        for (int i = 0; i < numOfCities; i++) {
            int reachableCitiesCount = 0;
            // Counting reachable cities for each city
            for (int j = 0; j < numOfCities; j++) {
                if (adjacencyMatrix[i][j] <= distanceThreshold) {
                    reachableCitiesCount++;
                }
            }
            // Updating optimal city if found with fewer reachable cities
            if (reachableCitiesCount <= minReachableCities) {
                minReachableCities = reachableCitiesCount;
                optimalCity = i;
            }
        }
        
        // Returning the optimal city
        return optimalCity;
    }
}      
```
