# Binary Tree Maximum Path Sum

Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain**at least one node**and does not need to go through the root.

For example:  
Given the below binary tree,

```text
       1
      / \
     2   3
```

Return`6`.

分析

single path从根节点出发往下走,一头固定 是辅助运算

singlePath = Math.max\(left.singlePath,right.singlePath\)+root.val; 再和0比，等于3个数取最大，最坏情况一个点都不取

maxpath 至少取一个点

maxPath=Math.max\(left.maxPath ,right.maxPath\)//左子树，右子树

maxPath=Math.max\(maxPath,left.singlePath+right.singlePath+root.val \)//再和跨越根节点的那条比

先算根节点到任意点singlePath，可不取所以最小是0。再任意点到任意点，必须要取值，所以极值是Integer.MIN\_VALUE

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
    private class ResultType{
        int simplePath;
        int multiPath;

        public ResultType(int simplePath, int multiPath){
            this.simplePath = simplePath;
            this.multiPath = multiPath;
        }        
    }
    public int maxPathSum(TreeNode root) {
        if(root == null)
            return 0;
        return helper(root).multiPath;        
    }

    public ResultType helper(TreeNode root){
        if(root == null)
            return new ResultType(0, Integer.MIN_VALUE);
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        //simple仅一头固定，所以只能左右中选一个
        int simplePath =  Math.max(Math.max(left.simplePath, right.simplePath) + root.val, 0);        

        int multiPath = Math.max(left.multiPath, right.multiPath);
        //multi可以两支都选
        multiPath = Math.max(multiPath, left.simplePath + right.simplePath + root.val);        

        return new ResultType(simplePath, multiPath);
    }
}
```

