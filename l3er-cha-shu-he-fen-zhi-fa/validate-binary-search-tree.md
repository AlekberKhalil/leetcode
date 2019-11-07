# Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys

  **less than**

  the node's key.

* The right subtree of a node contains only nodes with keys

  **greater than**

  the node's key.

* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```text
    2   / \  1   3
```

Binary tree

`[2,1,3]`

, return true.

**Example 2:**

```text
    1   / \  2   3
```

Binary tree

`[1,2,3]`

, return false.

分析

int 不够，需要long Long.MAX\_\_VALUE, Lo\_ng.MIN\_VALUE

```text
class Solution {    public boolean isValidBST(TreeNode root) {        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);    }    public boolean isValidBST(TreeNode root, long min, long max){        if(root == null)            return true;        if(root.val >= max ||root.val <= min){            return false;        }                return isValidBST(root.left, min, root.val) && isValidBST(root.right, root.val, max);    }}
```

