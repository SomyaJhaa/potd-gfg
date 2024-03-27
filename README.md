## GeeksForGeeks Problem Of The Day Solutions

This is my attempt to make the coding experience easier for you guys so that you can easily learn what to do in today's problem of the day.

## Today's 27-03=24 

## [Find shortest safe route in a matrix](https://www.geeksforgeeks.org/problems/find-shortest-safe-route-in-a-matrix/1)

## Intuition
The problem involves finding the shortest path from any cell with value 1 in the first column to any cell with value 1 in the last column, considering only cells with value 1 as passable and 0 as impassable. Landmines, represented by cells with value 0, block adjacent cells.

## Approach

**Marked Landmines :**
- I iterated through the grid.
- For each cell with value 0 (landmine), marked adjacent cells as impassable by setting their value to -1.

**Converted Marked Cells :**
- Converted all marked cells (value -1) back to passable cells (value 0).

**Breadth-First Search (BFS) :**
   - Initialized a 2D array to store distances from the starting point.
   - Initialized a queue for BFS traversal.
   - Enqueued cells from the first column with value 1 and set their distance to 0.
   - Performed BFS :
     - Dequeued a cell and explore its neighboring cells.
     - If a neighboring cell is valid, unvisited, and reachable, updated its distance and enqueue it.
   - Continued BFS until all reachable cells are visited or the queue is empty.

**Finded Shortest Path :**
   - Finded the minimum distance from any cell in the last column with value 1 to the destination.
   - If a destination cell cannot be reached, returned -1; otherwise, returned the minimum distance plus 1 as the shortest path length.

---
Have a look at the code , still have any confusion then please let me know in the comments

Keep Solving.:)

## Complexity
- Time complexity : $O( r*c )$
<!-- Add your time complexity here, e.g. $$O())$$ -->
$r$ : number of rows

$c$ : number of columns
- Space complexity : $O( r*c )$
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

## Code

```
//  User function Template for Java

class Solution {
    
    // Inner class to represent a cell in the grid
    static class Cell {
        int row, col;
        
        // Constructor to initialize row and column values of a cell
        Cell(int r, int c) {
            row = r;
            col = c;
        }
    }
    
    // Static variables to store the number of rows and columns in the grid
    static int ROWS;
    static int COLS;
    
    // Arrays to store possible moves in rows and columns (up, left, right, down)
    static int[] rowMoves = {-1, 0, 0, 1};
    static int[] colMoves = {0, -1, 1, 0};
    
    // Method to check if a given cell is within the grid boundaries
    static boolean isValid(int x, int y) {
        return (x >= 0 && y >= 0 && x < ROWS && y < COLS);
    }
    
    // Method to find the shortest path in the grid
    static int findShortestPath(int[][] grid) {
        ROWS = grid.length;
        COLS = grid[0].length;
        
        // Marking adjacent cells of landmines as -1
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS; j++) {
                if (grid[i][j] == 0) {
                    for (int k = 0; k < 4; k++) {
                        int nextRow = i + rowMoves[k];
                        int nextCol = j + colMoves[k];
                        if (isValid(nextRow, nextCol))
                            grid[nextRow][nextCol] = -1;
                    }
                }
            }
        }
        
        // Converting -1 cells back to 0
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS; j++) {
                if (grid[i][j] == -1)
                    grid[i][j] = 0;
            }
        }
        
        // Initializing a 2D array to store distances from the starting point
        int[][] distance = new int[ROWS][COLS];
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS; j++)
                distance[i][j] = -1;
        }
        
        // Initializing a queue for BFS traversal
        Queue<Cell> queue = new LinkedList<>();
        
        // Adding cells from the first column with value 1 to the queue and set their distance to 0
        for (int i = 0; i < ROWS; i++) {
            if (grid[i][0] == 1) {
                queue.add(new Cell(i, 0));
                distance[i][0] = 0;
            }
        }
        
        // Performing BFS to find shortest path
        while (!queue.isEmpty()) {
            Cell current = queue.poll();
            int d = distance[current.row][current.col];
            int x = current.row;
            int y = current.col;
            
            // Exploring neighboring cells
            for (int k = 0; k < 4; k++) {
                int newX = x + rowMoves[k];
                int newY = y + colMoves[k];
                
                // Checking if the neighboring cell is valid, unvisited, and reachable
                if (isValid(newX, newY) && distance[newX][newY] == -1 && grid[newX][newY] == 1) {
                  
                    // Updating distance and add the cell to the queue
                    distance[newX][newY] = d + 1;
                    queue.add(new Cell(newX, newY));
                }
            }
        }
        
        // Finding minimum distance to reach the last column
        int minDistance = Integer.MAX_VALUE;
        for (int i = 0; i < ROWS; i++) {
            if (grid[i][COLS - 1] == 1 && distance[i][COLS - 1] != -1) {
                minDistance = Math.min(minDistance, distance[i][COLS - 1]);
            }
        }
        
        // If destination cannot be reached, return -1; otherwise, returning the minimum distance plus 1
        if (minDistance == Integer.MAX_VALUE){
            return -1;
        } 
        else {
            return minDistance + 1;
        }
    }
}
```
