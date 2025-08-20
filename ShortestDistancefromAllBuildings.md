/*

https://leetcode.com/problems/shortest-distance-from-all-buildings/description/

You are given an m x n grid grid of values 0, 1, or 2, where:

each 0 marks an empty land that you can pass by freely,
each 1 marks a building that you cannot pass through, and
each 2 marks an obstacle that you cannot pass through.
You want to build a house on an empty land that reaches all buildings in the shortest total travel distance. You can only move up, down, left, and right.

Return the shortest travel distance for such a house. If it is not possible to build such a house according to the above rules, return -1.

The total travel distance is the sum of the distances between the houses of the friends and the meeting point.

 

Example 1:


Input: grid = [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]
Output: 7
Explanation: Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2).
The point (1,2) is an ideal empty land to build a house, as the total travel distance of 3+3+1=7 is minimal.
So return 7.
Example 2:

Input: grid = [[1,0]]
Output: 1
Example 3:

Input: grid = [[1]]
Output: -1
 

Constraints:

m == grid.length
n == grid[i].length
1 <= m, n <= 50
grid[i][j] is either 0, 1, or 2.
There will be at least one building in the grid.



*/

import java.util.LinkedList;
import java.util.Queue;

class Solution {

    /**
     * Finds the shortest total travel distance from an empty land ('0') to all buildings ('1').
     * @param grid The m x n grid of values 0, 1, or 2.
     * @return The shortest distance, or -1 if no such place exists.
     */
    public int shortestDistance(int[][] grid) {
        // Handle edge case of an invalid or empty grid.
        if (grid == null || grid.length == 0) {
            return -1;
        }

        // Get grid dimensions.
        int rows = grid.length;
        int cols = grid[0].length;

        // distanceSum[r][c] will store the sum of distances from cell (r,c) to all reachable buildings.
        int[][] distanceSum = new int[rows][cols];
        // reachCount[r][c] will store how many buildings can reach cell (r,c).
        int[][] reachCount = new int[rows][cols];
        // This will hold the total number of buildings in the grid.
        int totalBuildings = 0;

        // --- Step 1: Count total buildings and trigger BFS from each one ---

        // First pass: Iterate through the grid to find all buildings.
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // If the cell is a building...
                if (grid[i][j] == 1) {
                    totalBuildings++; // Increment the building counter.
                    // Start a BFS from this building to find distances to all empty lands.
                    bfs(grid, i, j, distanceSum, reachCount);
                }
            }
        }

        // --- Step 2: Find the optimal location with the minimum total distance ---

        // Initialize minDistance to the largest possible value.
        int minDistance = Integer.MAX_VALUE;

        // Second pass: Iterate through the grid to check every empty land cell.
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                // We are looking for an empty land cell...
                if (grid[i][j] == 0 && reachCount[i][j] == totalBuildings) {
                    // ...that is reachable by ALL buildings.
                    // If it is, we check if its total distance is a new minimum.
                    minDistance = Math.min(minDistance, distanceSum[i][j]);
                }
            }
        }

        // --- Step 3: Return the result ---

        // If minDistance was never updated, it means no valid spot was found.
        // Otherwise, return the minimum distance found.
        return minDistance == Integer.MAX_VALUE ? -1 : minDistance;
    }

    /**
     * Performs a Breadth-First Search (BFS) starting from a building.
     * It updates the distanceSum and reachCount grids for all reachable empty lands.
     */
    private void bfs(int[][] grid, int row, int col, int[][] distanceSum, int[][] reachCount) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        // The queue will store arrays of {row, col, distance}.
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{row, col, 0});
        
        // A 'visited' grid for the current BFS run to avoid cycles and redundant paths.
        boolean[][] visited = new boolean[rows][cols];
        visited[row][col] = true;

        // Movement directions: up, down, left, right.
        int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

        // Process the queue until it's empty.
        while (!queue.isEmpty()) {
            int[] current = queue.poll();
            int r = current[0];
            int c = current[1];
            int dist = current[2];

            // Explore all four neighbors.
            for (int[] dir : directions) {
                int newR = r + dir[0];
                int newC = c + dir[1];

                // Check if the neighbor is a valid, unvisited, empty land cell.
                if (newR >= 0 && newR < rows && newC >= 0 && newC < cols &&
                    !visited[newR][newC] && grid[newR][newC] == 0) {
                    
                    // Mark the neighbor as visited for this BFS.
                    visited[newR][newC] = true;
                    
                    // Add the distance from the building to this cell.
                    distanceSum[newR][newC] += dist + 1;
                    // Increment the count of buildings that can reach this cell.
                    reachCount[newR][newC]++;
                    
                    // Add the neighbor to the queue to explore from it later.
                    queue.offer(new int[]{newR, newC, dist + 1});
                }
            }
        }
    }
    
    // Main method for testing the solution.
    public static void main(String[] args) {
        Solution sol = new Solution();
        // Example grid with buildings(1), empty land(0), and obstacles(2).
        int[][] grid = {
            {1, 0, 2, 0, 1},
            {0, 0, 0, 0, 0},
            {0, 0, 1, 0, 0}
        };
        
        int result = sol.shortestDistance(grid);
        // The optimal location is at (1,2) with a total distance of 7.
        System.out.println("The shortest total travel distance is: " + result); // Expected output: 7
    }
}
