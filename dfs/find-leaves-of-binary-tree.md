# Find Leaves of Binary Tree

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

**Example:**

```text
Input: 
[1,2,3,4,5]


1
         / \
        2   3
       / \     
      4   5    


Output: 
[[4,5,3],[2],[1]]
```

**Explanation:**

1. Removing the leaves`[4,5,3]`would result in this tree:

```text
          1
         / 
        2
```

1. Now removing the leaf`[2]`would result in this tree:

```text
          1
```

1. Now removing the leaf`[1]`would result in the empty tree:

```text
          []
```

分析

和上面Nested list ii像，也是底部Level为0.dfs返回层数，里面res插入

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findLeaves(self, root: TreeNode) -> List[List[int]]:
        res = []

        self.dfs(root,res)
        return res

    def dfs(self, root: TreeNode, res:List[List[int]]) -> int:
        if not root:
            return -1

        level = 1+max(self.dfs(root.left,res),self.dfs(root.right,res))
        if len(res) - 1 < level:
            res+=[[root.val]] #注意【】的 level
        else:
            res[level]+=[root.val]
        return level
```

