# Lowest Common Ancestor of a Binary Tree\(递归）

Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.

According to the[definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants \(where we allow**a node to be a descendant of itself**\).”

Given the following binary tree: root = \[3,5,1,6,2,0,8,null,null,7,4\]

```text
        _______3______       /              \    ___5__          ___1__   /      \        /      \   6      _2       0       8         /  \         7   4
```

```text
Example 1:Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1Output: 3Explanation: The LCA of of nodes 5 and 1 is 3.Example 2:Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4Output: 5Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself             according to the LCA definition.
```

**Note:**

* All of the nodes' values will be unique.
* p and q are different and both values will exist in the binary tree.

分析：

不是搜索树。用的分治

注意tuple 可以这样 a,b = \(a,b\)

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def lowestCommonAncestor(self, root, p, q):        """        :type root: TreeNode        :type p: TreeNode        :type q: TreeNode        :rtype: TreeNode        """        if not root:            return root        if root.val == p.val:            return p        if root.val == q.val:            return q        left =  self.lowestCommonAncestor(root.right,p,q)        right =  self.lowestCommonAncestor(root.left,p,q)        if not left:            return right        if not right:            return left        if left.val == p.val and right.val == q.val or left.val == q.val and right.val == p.val:            return root
```

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def lowestCommonAncestor(self, root, p, q):        if root in (None, p, q): return root        left,right = (self.lowestCommonAncestor(kid, p, q)                for kid in (root.left, root.right))        return root if left and right else left or right
```

