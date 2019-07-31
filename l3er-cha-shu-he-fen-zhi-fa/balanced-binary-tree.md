# Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees ofeverynode never differ by more than 1.

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
    public boolean isBalanced(TreeNode root) {
        if(root == null)
            return true;
        return height(root) >= 0;
    }

    public int height(TreeNode root){
        if(root == null)
            return 0;
        int left = height(root.left);
        int right = height(root.right);
        if(left < 0 || right < 0 || Math.abs(left - right) > 1)
            return -1;
        return 1 + Math.max(left, right);
    }
}
```

```text
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null)
            return true;
        if(!isBalanced(root.left) || !isBalanced(root.right) || Math.abs(height(root.left) - height(root.right)) > 1)
            return false;
        return true;
    }

    public int height(TreeNode root){
        if(root == null)
            return 0;
        int left = height(root.left);
        int right = height(root.right);

        return 1 + Math.max(left, right);
    }
}
```

