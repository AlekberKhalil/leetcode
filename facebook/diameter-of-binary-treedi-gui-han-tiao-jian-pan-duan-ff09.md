# Diameter of Binary Tree\(递归含条件判断）

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the**longest**path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**  
Given a binary tree

```text
          1         / \        2   3       / \           4   5
```

Return**3**, which is the length of the path \[4,2,1,3\] or \[5,2,1,3\].

**Note:**The length of path between two nodes is represented by the number of edges between them.

分析

递归返回depth,但是同时在递归里更新全局变量diameter，不返回而已。这里把getDepth函数作为内置函数

注意内置函数写法，里面不含任何self，除了使用的全局变量。

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def diameterOfBinaryTree(self, root):        """        :type root: TreeNode        :rtype: int        """        self.d = 0        def depth(root):            if not root:                return 0            l,r = depth(root.left),depth(root.right)            self.d = max(self.d,l+r)            return 1+ max(l,r)        depth(root)        return self.d
```

