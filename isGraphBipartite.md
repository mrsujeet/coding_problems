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


 The input looks like a “2-D array,” but it’s **not an adjacency matrix**—it’s an **adjacency list encoded as array-of-arrays**:

* **Adjacency list idea:** for each node `u`, store a list of its actual neighbors.
* **What you’re given:** `int[][] graph` where **`graph[u]` is exactly that neighbor list**. Its length equals the degree of `u`, not `n`.

### Example A (your Example 2)

```
graph = [
  [1,3],   // neighbors of 0 → edges: (0,1), (0,3)
  [0,2],   // neighbors of 1 → edges: (1,0), (1,2)
  [1,3],   // neighbors of 2 → edges: (2,1), (2,3)
  [0,2]    // neighbors of 3 → edges: (3,0), (3,2)
]
```

Same edges (undirected ⇒ symmetric lists):
{ (0,1), (0,3), (1,2), (2,3) }.

How you iterate neighbors of `u`:

```java
for (int v : graph[u]) {
    // v is a neighbor of u
}
```


*/

import java.util.*;

class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n]; // 0 = uncolored, +1 and -1 are the two colors

        for (int s = 0; s < n; s++) {
            if (color[s] != 0) continue;         // already explored component
            color[s] = 1;
            Deque<Integer> q = new ArrayDeque<>();
            q.add(s);

            while (!q.isEmpty()) {
                int u = q.poll();
                for (int v : graph[u]) {          // iterate actual neighbors of u
                    if (color[v] == 0) {
                        color[v] = -color[u];     // opposite color
                        q.add(v);
                    } else if (color[v] == color[u]) {
                        return false;             // edge connects same color → not bipartite
                    }
                }
            }
        }
        return true;
    }
}
}

