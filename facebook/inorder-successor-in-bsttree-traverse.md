# Inorder Successor in BST\(tree traverse\)

Given a binary search tree \([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)\) and a node in it, find the in-order successor of that node in the BST.

If the given node has no in-order successor in the tree, return`null`.

## Example

Given tree =`[2,1]`and node =`1`:

```text
  2
 /
1
```

return node`2`.

Given tree =`[2,1,3]`and node =`2`:

```text
  2
 / \
1   3
```

return node`3`.

## Challenge

O\(h\), where h is the height of the BST.

## Notice

It's guaranteed\_p\_is one node in the given tree. \(You can directly compare the memory address to find p\)

分析

就是中序遍历加条件

```text
"""
Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
"""


class Solution:
    """
    @param: root: The root of the BST.
    @param: p: You need find the successor node of p.
    @return: Successor of p.
    """
    def inorderSuccessor(self, root, p):
        # write your code here
        stack = []
        cur = root
        prev = None
        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            cur = stack.pop()
            if prev and prev.val == p.val:
                return cur
            prev = cur
            cur = cur.right
        return None
```

递归

这里相当于二分，找到第一个root.val&gt;p.val

```text
"""
Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
"""


class Solution:
    """
    @param: root: The root of the BST.
    @param: p: You need find the successor node of p.
    @return: Successor of p.
    """
    def inorderSuccessor(self, root, p):
        # write your code here
        if not root or not p:
            return None
        if root.val<=p.val:
            return self.inorderSuccessor(root.right,p)
        else:
            left = self.inorderSuccessor(root.left,p)
            return left if left else root
```

