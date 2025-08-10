/*
https://leetcode.com/problems/binary-tree-right-side-view/editorial/
iven the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

 

Example 1:

Input: root = [1,2,3,null,5,null,4]

Output: [1,3,4]

Explanation:



Example 2:

Input: root = [1,2,3,4,null,null,null,5]

Output: [1,3,4,5]

Explanation:



Example 3:

Input: root = [1,null,3]

Output: [1,3]

Example 4:

Input: root = []

Output: []

 

Constraints:

The number of nodes in the tree is in the range [0, 100].
-100 <= Node.val <= 100

*/


import java.util.*;

// Binary tree node definition
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int v) { val = v; }
}

class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> view = new ArrayList<>();
        if (root == null) return view;   // empty tree → empty view

        // Standard BFS queue
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        // Process the tree level by level
        while (!q.isEmpty()) {
            int levelSize = q.size();    // number of nodes in the current level

            // Traverse all nodes in this level
            for (int i = 0; i < levelSize; i++) {
                TreeNode cur = q.poll();

                // Enqueue children for the next level (left first, then right)
                if (cur.left != null)  q.offer(cur.left);
                if (cur.right != null) q.offer(cur.right);

                // The last node we pop at this level is the rightmost one
                if (i == levelSize - 1) {
                    view.add(cur.val);
                }
            }
        }

        return view;
    }
}


