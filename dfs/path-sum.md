# Path  Sum II

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and

`sum = 22`

,

```text
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

return

```text
[
   [5,4,11,2],
   [5,8,4,5]
]
```

分析

dfs开始就加入path，结束移除。以root为例，并且判断是否叶子节点和加入val，然后决定是否加入ret。

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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> ret = new ArrayList<>();
        if(root == null)
            return ret;
        List<Integer> path = new ArrayList<Integer>();
        dfs(root, sum, path, ret);
        return ret;
    }
   public void dfs(TreeNode root, int sum, List<Integer> path, List<List<Integer>> ret){
       path.add(root.val);//开始就加入
       //是叶节点并且此处加入val值
       if(root.left == null && root.right == null && sum - root.val == 0){
           ret.add(new ArrayList<Integer>(path));
       }           
       //检测是否存在left   
       if(root.left != null){
           dfs(root.left, sum - root.val, path, ret);
       }
       if(root.right != null){
           dfs(root.right, sum - root.val, path, ret);
       }
       path.remove(path.size() - 1);//结束移除
   }
}
```

