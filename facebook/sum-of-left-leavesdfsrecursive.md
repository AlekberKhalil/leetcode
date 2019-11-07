# Sum of Left Leaves\(递归和分治，dfs，树\)

```text
Find the sum of all left leaves in a given binary tree.Example:    3   / \  9  20    /  \   15   7There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

分析

开始合在一个函数里，然后sum = root.left........ --- + sumOfLeftLeaves\(left\)+sumOfLeftLeaves\(right\), return sum

错误点是递归函数里只能对一个节点运算，这里既算了root又结合了左右递归的结果，重复了。

递归：不需要返回值，但是需要全局变量来存答案。当前root对全局变量操作，然后进入左右树递归。

```text
class Solution:    sum = 0    def sumOfLeftLeaves(self, root):        """        :type root: TreeNode        :rtype: int        """        self.preOrder(root)        return self.sum    def preOrder(self, root):        if not root:            return        left = root.left        if left and not left.left and not left.right:                self.sum += left.val        self.preOrder(root.left)        self.preOrder(root.right)
```

分治：需要返回值，当前root和左右子树综合得到答案。

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def sumOfLeftLeaves(self, root):        """        :type root: TreeNode        :rtype: int        """        return self.helper(TreeNode(-1),root)    def helper(self,parent,root):        if not root:            return 0        if not root.left and not root.right:            if root == parent.left:                return root.val        l = self.helper(root, root.left)        r = self.helper(root, root.right)        return l + r
```

