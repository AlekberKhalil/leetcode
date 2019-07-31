# Maximum Depth of N-ary Tree

Given a n-ary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example, given a`3-ary`tree:

![](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

We should return its max depth, which is 3.

**Note:**

1. The depth of the tree is at most

   `1000`

   .

2. The total number of nodes is at most

   `5000`

分析

DFS

```text
"""
# Definition for a Node.
class Node:
    def __init__(self, val, children):
        self.val = val
        self.children = children
"""
class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0

        return 1+max([self.maxDepth(x) for x in root.children] or [0])
```

