# Binary Tree Zigzag Level Order Traversal

Given a binary tree, return thezigzag level ordertraversal of its nodes' values. \(ie, from left to right, then right to left for the next level and alternate between\).

For example:  
Given binary tree`[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:

```text
[
  [3],
  [20,9],
  [15,7]
]
```

分析

设置index每层变化

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> ret = new ArrayList<>();
        if(root == null)
        return ret;

        bfs(root, ret);
        return ret;
    }

    public void bfs(TreeNode root, List<List<Integer>> ret){
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        int index = 0;
        while(!q.isEmpty()){
            List<Integer> level = new ArrayList<Integer>();
            int size = q.size();
            for(int i = 0; i < size; i ++){
                TreeNode cur = q.poll();
                if(index % 2 == 0){
                    level.add(cur.val);
                }else{
                    level.add(0, cur.val);
                }

                if(cur.left != null){
                    q.offer(cur.left);
                }
                if(cur.right != null){
                    q.offer(cur.right);
                }
            }
            ret.add(level);
            index ++;
        }
    }
}
```

isEmpty 不是!=null

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null)
            return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        boolean x = true;
        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> level = new ArrayList<>();
            for(int i = 0; i < size; i ++){
                TreeNode cur = q.poll();
                if(x)
                    level.add(cur.val);
                else
                    level.add(0,cur.val);
                if(cur.left != null)
                    q.offer(cur.left);
                if(cur.right != null)
                    q.offer(cur.right);                       
            }
            x = !x;
            res.add(level);
            
        }
        return res;
    }
}
```



