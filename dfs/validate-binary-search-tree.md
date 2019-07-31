# Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys

  **less than** the node's key.

* The right subtree of a node contains only nodes with keys

  **greater than** the node's key.

* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```text
    2
   / \
  1   3
```

Binary tree`[2,1,3]`, return true.

**Example 2:**

```text
    1
   / \
  2   3
```

Binary tree`[1,2,3]`, return false.

分析

递归传入最大值和最小值。用Long

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
    public boolean isValidBST(TreeNode root) {      
        return helper(root, Long.MAX_VALUE, Long.MIN_VALUE);
    }

    boolean helper(TreeNode root, long max, long min){
        if(root == null){
            return true;
        }
        if(root.val >= max || root.val <= min){
            return false;
        }
        return helper(root.left, root.val, min) && helper(root.right, max, root.val);
    }
}
```

