/*
https://leetcode.com/problems/is-graph-bipartite/description/
https://leetcode.com/problems/is-graph-bipartite/editorial/

There is an undirected graph with n nodes, where each node is numbered between 0 and n - 1. You are given a 2D array graph, where graph[u] is an array of nodes that node u is adjacent to. More formally, for each v in graph[u], there is an undirected edge between node u and node v. The graph has the following properties:

There are no self-edges (graph[u] does not contain u).
There are no parallel edges (graph[u] does not contain duplicate values).
If v is in graph[u], then u is in graph[v] (the graph is undirected).
The graph may not be connected, meaning there may be two nodes u and v such that there is no path between them.
A graph is bipartite if the nodes can be partitioned into two independent sets A and B such that every edge in the graph connects a node in set A and a node in set B.

Return true if and only if it is bipartite.

 

Example 1:


Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
Output: false
Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
Example 2:


Input: graph = [[1,3],[0,2],[1,3],[0,2]]
Output: true
Explanation: We can partition the nodes into two sets: {0, 2} and {1, 3}.
 

Constraints:

graph.length == n
1 <= n <= 100
0 <= graph[u].length < n
0 <= graph[u][i] <= n - 1
graph[u] does not contain u.
All the values of graph[u] are unique.
If graph[u] contains v, then graph[v] contains u.

<img width="773" height="574" alt="image" src="https://github.com/user-attachments/assets/44307399-e3d7-4e9a-baa4-610b56a2205c" />


*/

import java.util.LinkedList;
import java.util.Queue;

class Solution {
    /**
     * Determines if an undirected graph is bipartite using a two-coloring BFS approach.
     *
     * @param graph An adjacency list representation of the graph.
     * @return True if the graph is bipartite, False otherwise.
     */
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        // 0: uncolored, 1: color A, -1: color B
        int[] colors = new int[n]; 

        // This outer loop is necessary for graphs that may be disconnected.
        for (int i = 0; i < n; i++) {
            // If the node is already colored, its component has been visited.
            if (colors[i] != 0) {
                continue;
            }

            // Start BFS for this uncolored component.
            Queue<Integer> queue = new LinkedList<>();
            queue.add(i);
            colors[i] = 1; // Start by coloring the first node with color 1.

            while (!queue.isEmpty()) {
                int u = queue.poll();

                // Check all neighbors of the current node.
                for (int v : graph[u]) {
                    if (colors[v] == 0) {
                        // If the neighbor is uncolored, assign the opposite color.
                        colors[v] = -colors[u];
                        queue.add(v);
                    } else if (colors[v] == colors[u]) {
                        // If the neighbor has the same color, a conflict is found.
                        return false; 
                    }
                }
            }
        }

        // If the loops complete without any conflicts, the graph is bipartite.
        return true;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();

        // Example 1: A bipartite graph (a square)
        int[][] graph1 = {{1, 3}, {0, 2}, {1, 3}, {0, 2}};
        System.out.println("Graph 1 is bipartite: " + sol.isBipartite(graph1)); // Output: true

        // Example 2: A non-bipartite graph (a triangle)
        int[][] graph2 = {{1, 2}, {0, 2}, {0, 1}};
        System.out.println("Graph 2 is bipartite: " + sol.isBipartite(graph2)); // Output: false
    }
}
