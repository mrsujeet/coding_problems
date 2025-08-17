/*

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/

Given the root of a binary tree, flatten the tree into a "linked list":

The "linked list" should use the same TreeNode class where the right child pointer points to the next node in the list and the left child pointer is always null.
The "linked list" should be in the same order as a pre-order traversal of the binary tree.
 

Example 1:


Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
Example 2:

Input: root = []
Output: []
Example 3:

Input: root = [0]
Output: [0]
 

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-100 <= Node.val <= 100


*/
/*
Why reverse order works

In the final flattened list, each node’s .right must point to the next node in preorder.

If you traverse in normal preorder (root→left→right), when you stand on a node you don’t yet have the fully built list of “what comes next,” so you’d need extra bookkeeping (a stack).

If you traverse in reverse preorder (right→left→root), by the time you reach a node, you have already flattened and chained everything that should appear after it. We keep the head of that suffix in a single pointer prev. Then:

node.right = prev

node.left = null

prev = node

That’s the whole trick.
*/

class Solution {
    private TreeNode prev = null; // head of the already-flattened suffix (nodes that come AFTER current in preorder)

    public void flatten(TreeNode root) {
        // Reverse-preorder: process right, then left, then the node itself.
        if (root == null) return;

        flatten(root.right);  // flatten everything that comes after the left subtree in preorder
        flatten(root.left);   // flatten left subtree next

        // Now prev is the head of the flattened list of all nodes that should follow 'root' in preorder.
        root.right = prev;    // stitch current node to that suffix
        root.left = null;     // left must be null in the final list
        prev = root;          // move prev up: new suffix head is now 'root'
    }
}
