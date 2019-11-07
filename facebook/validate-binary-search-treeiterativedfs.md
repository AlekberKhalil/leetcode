# Validate Binary Search Tree\(iterative,dfs\)

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
Input:    2   / \  1   3Output: true
```

**Example 2:**

```text
    5   / \  1   4     / \    3   6Output: falseExplanation: The input is: [5,1,4,null,null,3,6]. The root node's value             is 5 but its right child's value is 4.
```

分析

中序遍历 while

```text
# Definition for a binary tree node.# class TreeNode(object):#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution(object):    def isValidBST(self, root):        """        :type root: TreeNode        :rtype: bool        """        stack = []        cur = root        prev = None        while cur or stack:            while cur:                stack.append(cur)                cur = cur.left            cur = stack.pop()            if prev and cur.val<=prev.val:                return False            prev = cur            cur = cur.right        return True
```

dfs

用root.val 传入dfs参数，作为最大值最小值

```text
float('-inf'),float('inf')
```

```text
# Definition for a binary tree node.# class TreeNode(object):#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution(object):    def isValidBST(self, root):        """        :type root: TreeNode        :rtype: bool        """        return self.helper(root,float('-inf'),float('inf'))    def helper(self,root,minn,maxx):        if not root:            return True        if root.val >= maxx or root.val <= minn:            return False        return self.helper(root.left,minn,root.val) and self.helper(root.right,root.val,maxx)
```

