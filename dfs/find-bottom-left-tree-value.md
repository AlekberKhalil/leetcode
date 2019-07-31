# Find Bottom Left Tree Value

Given a binary tree, find the leftmost value in the last row of the tree.

**Example 1:**

```text
Input:

    2
   / \
  1   3

Output:
1
```

**Example 2:**

```text
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

**Note:**You may assume the tree \(i.e., the given root node\) is not**NULL**.

分析

bfs就是层遍历，注意每次弹出的是q\[0\]

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        q = [root]
        res = None
        while q:
            size = len(q)
            res = q[0]
            for i in range(size):
                cur = q.pop(0)
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
        return res.val
```

DFS

哪个先突破新高度就是那个node，每次都是左边先

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findBottomLeftValue(self, root: TreeNode) -> int:
        res,depth = root.val, 1
        def dfs(root:TreeNode,d:int):
            nonlocal depth,res
            if not root:
                return
            if depth < d:
                depth = d
                res = root.val
            dfs(root.left,d+1)
            dfs(root.right,d+1)
        dfs(root,1)
        return res
```

