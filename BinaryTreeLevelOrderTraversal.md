/*
[binary-tree-level-order-traversa](https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/1731840004/)

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

 

Example 1:


Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []
 

Constraints:

The number of nodes in the tree is in the range [0, 2000].
-1000 <= Node.val <= 1000

*/



public List<List<Integer>> levelOrder(TreeNode root) {

        List <List<Integer>> list =new ArrayList<>();
        if(root ==null) return list;

        Queue<TreeNode> q= new LinkedList<>();

        q.offer(root);

        while(!q.isEmpty()){
            int size= q.size();
           
            List<Integer> level= new ArrayList<>();

            for(int i=0; i<size; i++){
                 TreeNode node =q.poll();
                level.add(node.val);

                if(node.left!=null){
                    q.add(node.left);
                }

                if(node.right!=null){
                     q.add(node.right);
                }

            }
            list.add(level);

        }
        return list;
    }
