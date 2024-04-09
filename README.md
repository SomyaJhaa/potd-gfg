## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 09-04-24

## [Minimum Points To Reach Destination](https://www.geeksforgeeks.org/problems/minimum-points-to-reach-destination0540/1)

## Intuition
The problem requires finding the minimum points needed to traverse a grid from top-left to bottom-right, where each cell has positive or negative points. I need to ensure that the accumulated points never drop below 1 during traversal.

## Approach

I used Dynamic Programming with Memoization.
- Started from the bottom-right corner and recursively explore paths towards the top-left corner.
- Kept track of the minimum points required at each cell.
- Memoized computed results to avoid redundant computations.
- Returned the minimum points required to reach the bottom-right corner.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O(n*m)$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$n$ : number of rows (given)

$m$ : number of columns (given)
- Space complexity : $O(n*m)$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Method to calculate the minimum points required
    public int minPoints(int[][] pointsArray, int numRows, int numCols) {
        
        // Memoization array to store already computed results
        int[][] memo = new int[numRows][numCols];
        for (int[] row : memo) {
            Arrays.fill(row, Integer.MIN_VALUE);
        }
        
        // Call the recursive DFS method to compute minimum points
        return calculateDFS(0, 0, pointsArray, numRows, numCols, memo);
    }

    // Recursive DFS method to compute minimum points
    private int calculateDFS(int row, int col, int[][] points, int numRows, int numCols, int[][] memo) {
        
        // If reached the bottom-right corner of the grid
        if (row == numRows - 1 && col == numCols - 1) {
            // Return 1 if the current cell value is positive, otherwise return the absolute value plus 1
            return points[row][col] > 0 ? 1 : Math.abs(points[row][col]) + 1;
        }
        
        // If the result for the current cell is already computed, return it
        if (memo[row][col] != Integer.MIN_VALUE) {
            return memo[row][col];
        }
        
        // Initialize minimum points required for the current cell to the maximum value
        int minPoints = Integer.MAX_VALUE;
        
        // Try moving right if it's within the grid boundaries
        if (col + 1 < numCols) {
            // Calculate the points required for moving right and update the minimum points accordingly
            int right = -points[row][col] + calculateDFS(row, col + 1, points, numRows, numCols, memo);
            minPoints = Math.min(minPoints, right);
        }
        
        // Try moving down if it's within the grid boundaries
        if (row + 1 < numRows) {
            // Calculate the points required for moving down and update the minimum points accordingly
            int down = -points[row][col] + calculateDFS(row + 1, col, points, numRows, numCols, memo);
            minPoints = Math.min(minPoints, down);
        }
        
        // Store the computed minimum points for the current cell in the memoization array
        memo[row][col] = minPoints <= 0 ? 1 : minPoints;
        
        // Return the minimum points required for the current cell
        return memo[row][col];
    }
}
```
