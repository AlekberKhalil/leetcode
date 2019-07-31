# Binary Tree Level Order Traversal II

Given a binary tree, return thebottom-up level ordertraversal of its nodes' values. \(ie, from left to right, level by level from leaf to root\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```text
[
  [15,7],
  [9,20],
  [3]
]
```

分析

和前面一提区别就是arraylist.add（index，value\)

```text
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<>();
        if(root == null)
            return ret;

        bfs(root, ret);
        return ret;
    }

    public void bfs(TreeNode root, List<List<Integer>> ret){
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        while(!q.isEmpty()){
        List<Integer> level = new ArrayList<Integer>();
        int size = q.size();
        for(int i = 0; i < size; i ++){
            TreeNode cur = q.poll();
            level.add(cur.val);
            if(cur.left != null){
                q.offer(cur.left);
            }
            if(cur.right != null){
                q.offer(cur.right);
            }
        }
        ret.add(0, level);
        }
    }
}
```

