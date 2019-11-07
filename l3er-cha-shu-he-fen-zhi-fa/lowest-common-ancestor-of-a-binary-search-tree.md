# Lowest Common Ancestor of a Binary Search Tree

Given a binary search tree \(BST\), find the lowest common ancestor \(LCA\) of two given nodes in the BST.

According to the[definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants \(where we allow**a node to be a descendant of itself**\).”

```text
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```

For example, the lowest common ancestor \(LCA\) of nodes`2`and`8`is`6`. Another example is LCA of nodes`2`and`4`is`2`, since a node can be a descendant of itself according to the LCA definition.

分析

还是分治法，左边和右边都有的话，返回根，否则哪边不空返回哪边。

```text
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null)
            return null;
        if(root == q)
            return q;
        if(root == p)
            return p;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left != null && right != null)
            return root;
        if(left != null)
            return left;
        else
            return right;
    }
```

一行解决，根据二叉树左右子树大小的值的性质

```text
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null)
            return null;
        if((root.val - p.val) *(root.val - q.val) < 1){
            return root;
        }
        return lowestCommonAncestor(root.val < p.val ? root.right : root.left, p, q);
    }
```

