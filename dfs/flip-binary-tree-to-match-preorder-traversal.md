# Flip Binary Tree To Match Preorder Traversal

Given a binary tree with`N`nodes, each node has a different value from `{1, ..., N}`.

A node in this binary tree can be_flipped_ by swapping the left child and the right child of that node.

Consider the sequence of `N`values reported by a preorder traversal starting from the root. Call such a sequence of`N`values the _voyage_ of the tree.

\(Recall that a_preorder traversal_ of a node means we report the current node's value, then preorder-traverse the left child, then preorder-traverse the right child.\)

Our goal is to flip the**least number**of nodes in the tree so that the voyage of the tree matches the`voyage`we are given.

If we can do so, then return a list of the values of all nodes flipped. You may return the answer in any order.

If we cannot do so, then return the list`[-1]`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/02/1219-01.png)

```text
Input: root = [1,2], voyage = [2,1]Output: [-1]
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/02/1219-02.png)

```text
Input: root = [1,2,3], voyage = [1,3,2]Output: [1]
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/01/02/1219-02.png)

```text
Input: root = [1,2,3], voyage = [1,2,3]Output: []
```

**Note:**

```text
1 <= N <= 100
```

分析

preorder遍历返回bool。比较root and root left的值，不对的话直接**翻转**继续dfs

```text
Explanation:Global integer i indicates next index in voyage v.If current node == null, it's fine, we return trueIf current node.val != v[i], doesn't match wanted value, return falseIf left child exist but don't have wanted value, flip it with right child.
```

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def flipMatchVoyage(self, root: TreeNode, voyage: List[int]) -> List[int]:        i = 0        res =[]        def dfs(node):            nonlocal i            if not node:                return True            if node.val != voyage[i]:                return False            i += 1            if node.left and node.left.val != voyage[i]:                res.append(node.val)                node.left,node.right = node.right,node.left            return dfs(node.left) and dfs(node.right)        return res if dfs(root) else [-1]
```

