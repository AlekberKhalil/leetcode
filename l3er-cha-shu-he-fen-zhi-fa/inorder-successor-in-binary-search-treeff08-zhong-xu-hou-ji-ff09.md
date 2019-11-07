# Inorder Successor in Binary Search Tree（中序后继）

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

Note: If the given node has no in-order successor in the tree, return `null`.

## Successor

分析

利用bst左右子树和root大小关系

iterative

```text
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode ret = null;
        while(root != null){
            if(root.val > p.val){
                ret = root;
                root = root.left;
            }else{
                root = root.right;
            }
        }

        return ret;
    }
```

recursive

```text
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root == null)
        return null;
        if(root.val > p.val){
            TreeNode left = inorderSuccessor(root.left, p);
            return left != null ? left : root;
        }else{
            return inorderSuccessor(root.right, p);
        }
    }
```

## Predecessor

iterative

```text
public TreeNode predecessor(TreeNode root, TreeNode p) {
    TreeNode ret = null;
    while(root != null){
        if(root.val < p.val){
            ret = root;
            root = root.right;
        }else{
            root = root.left;           
        }
    }
    return ret;
}
```

recursive

```text
public TreeNode predecessor(TreeNode root, TreeNode p) {
    if(root == null)
        return null;

    if(root.val < p.val){
        TreeNode right =  predecessor(root.right, p);
        return right != null : right : root;
    }elsel{
        return predecessor(root.left, p);

    }

}
```

