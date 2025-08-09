/*
https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/

Given the root of a binary tree, return the vertical order traversal of its nodes' values. (i.e., from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
Example 2:


Input: root = [3,9,8,4,0,1,7]
Output: [[4],[9],[3,0,1],[8],[7]]
Example 3:


Input: root = [1,2,3,4,10,9,11,null,5,null,null,null,null,null,null,null,6]
Output: [[4],[2,5],[1,10,9,6],[3],[11]]


Approach:

Alright — let’s walk through **BFS vertical order traversal** for

```
    3
   / \
  9  20
     / \
    15  7
```

We’ll track:

* **`nodeQ`** → nodes to visit
* **`colQ`** → their column numbers
* **`map`** → `column → list of values`

---

### **Step 0 – Initialization**

```
nodeQ = [3]
colQ  = [0]        // root at column 0
map   = {}
```

---

### **Step 1 – Process node 3**

```
node = 3, col = 0

map[0] = [3]       // add 3 to column 0

Enqueue left child (9) at col = -1
Enqueue right child (20) at col = 1

nodeQ = [9, 20]
colQ  = [-1, 1]
map   = { 0: [3] }
```

---

### **Step 2 – Process node 9**

```
node = 9, col = -1

map[-1] = [9]

(No children to enqueue)

nodeQ = [20]
colQ  = [1]
map   = { -1: [9], 0: [3] }
```

---

### **Step 3 – Process node 20**

```
node = 20, col = 1

map[1] = [20]

Enqueue left child (15) at col = 0
Enqueue right child (7) at col = 2

nodeQ = [15, 7]
colQ  = [0, 2]
map   = { -1: [9], 0: [3], 1: [20] }
```

---

### **Step 4 – Process node 15**

```
node = 15, col = 0

map[0] = [3, 15]

(No children)

nodeQ = [7]
colQ  = [2]
map   = { -1: [9], 0: [3, 15], 1: [20] }
```

---

### **Step 5 – Process node 7**

```
node = 7, col = 2

map[2] = [7]

(No children)

nodeQ = []
colQ  = []
map   = { -1: [9], 0: [3, 15], 1: [20], 2: [7] }
```

---

✅ **Final Output**
Sort columns: `-1, 0, 1, 2`

```
[[9], [3, 15], [20], [7]]


*/


import java.util.*;

/** Definition for a binary tree node. */
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        // Map: column index -> list of node values (top->bottom, left->right)
        Map<Integer, List<Integer>> colMap = new HashMap<>();

        // Two parallel queues for BFS:
        // nodeQ holds nodes; colQ holds their corresponding column indices
        Queue<TreeNode> nodeQ = new LinkedList<>();
        Queue<Integer>  colQ  = new LinkedList<>();

        nodeQ.offer(root);
        colQ.offer(0);                 // root is at column 0

        int minCol = 0, maxCol = 0;    // track range of columns we visit

        while (!nodeQ.isEmpty()) {
            TreeNode node = nodeQ.poll();
            int col = colQ.poll();

            // Append this node's value to its column's bucket
            if (!colMap.containsKey(col)) {
                  colMap.put(col, new ArrayList<>());
              }
              colMap.get(col).add(node.val);


            // Track column bounds so we can read columns left->right at the end
            minCol = Math.min(minCol, col);
            maxCol = Math.max(maxCol, col);

            // Enqueue children with their column indices:
            // Left child is one column to the left; right child is one to the right.
            if (node.left != null) {
                nodeQ.offer(node.left);
                colQ.offer(col - 1);
            }
            if (node.right != null) {
                nodeQ.offer(node.right);
                colQ.offer(col + 1);
            }
        }

        // Build result from leftmost column to rightmost column
        for (int c = minCol; c <= maxCol; c++) {
            result.add(colMap.get(c));
        }
        return result;
    }
}
