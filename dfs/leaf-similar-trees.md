# Leaf-Similar Trees

Consider all the leaves of a binary tree. From left to right order, the values of those leaves form a_leaf value sequence._

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/16/tree.png)

For example, in the given tree above, the leaf value sequence is`(6, 7, 4, 9, 8)`.

Two binary trees are considered_leaf-similar_ if their leaf value sequence is the same.

Return`true`if and only if the two given trees with head nodes`root1`and`root2`are leaf-similar.

**Note:**

* ```text
  Both of the given trees will have between 1 and 100 nodes.
  ```

分析

dfs返回叶子列表

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def leafSimilar(self, root1: TreeNode, root2: TreeNode) -> bool:

        def dfs(root):
            if not root:
                return []
            if not root.left and not root.right:
                return [root.val]

            return dfs(root.left) + dfs(root.right)
        return dfs(root1) == dfs(root2)
```

