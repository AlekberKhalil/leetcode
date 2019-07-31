# Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

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
         /  \      \
        7    2      1
```

return true, as there exist a root-to-leaf path`5->4->11->2`which sum is 22.

分析

DFS

```text
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;
        return dfs(root, sum);
    }

    public boolean dfs(TreeNode root, int sum){

        if(root.left == null && root.right == null && root.val == sum){          
             return true;            
        }
        boolean ret = false;

        if(root.left != null){
           ret |= dfs(root.left, sum - root.val);
        }

        if(root.right != null){
           ret |= dfs(root.right, sum - root.val);
        }

        return ret;
    }       

}
```

分治法

```text
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;
        if(root.left == null && root.right == null)
            return root.val == sum;
        return hasPathSum(root.left, sum - root.val)
            || hasPathSum(root.right, sum - root.val);
    }   
}
```

