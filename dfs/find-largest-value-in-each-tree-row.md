# Find Largest Value in Each Tree Row

You need to find the largest value in each row of a binary tree.

**Example:**

```text
Input:


          1
         / \
        3   2
       / \   \  
      5   3   9 


Output:
 [1, 3, 9]
```

分析

dfs

d和Len\(res\)比较，不够就加，够就比较得最大

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def largestValues(self, root: TreeNode) -> List[int]:
        res = []
        def dfs(root:TreeNode, d:int):
            if not root:
                return
            if len(res) < d:
                res.append(root.val)
            elif res[d-1] < root.val:                
                res[d-1] = root.val
            dfs(root.left,d+1)
            dfs(root.right,d+1)
        dfs(root,1)
        return res
```

BFS

层遍历一定要pop\(0\)从前面弹起，因为后面是不合条件的子树。

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def largestValues(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        res = []
        q = [root]
        while q:
            size = len(q)
            curmax = float('-inf')
            for i in range(size):
                cur = q.pop(0) #必须要从前面开始 因为后面的是新加的子树
                if cur.val > curmax:
                    curmax = cur.val
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            res.append(curmax)
        return res
```

