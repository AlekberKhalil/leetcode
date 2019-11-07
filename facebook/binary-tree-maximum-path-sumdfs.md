# Binary Tree Maximum Path Sum\(dfs\)

Given a**non-empty**binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain**at least one node**and does not need to go through the root.

**Example 1:**

```text
Input:
 [1,2,3]


1
/ \
2
3
Output:
 6
```

**Example 2:**

```text
Input:
 [-10,9,20,null,null,15,7]

   -10
   / \
  9  
20
/  \
15   7
Output:
 42
```

分析

dfs做2个事情：

1、max是答案，每次dfs更新

2、返回的是单个Branch的值

[https://leetcode.com/problems/binary-tree-maximum-path-sum/discuss/39775/Accepted-short-solution-in-Java](https://leetcode.com/problems/binary-tree-maximum-path-sum/discuss/39775/Accepted-short-solution-in-Java)

```text
Idea & Cases Explanation. Java + recursion
At first, I think 2 parameters should be return in recursion. Then I find that we only need to update max once, so I move max to be a member parameter.

Basic idea:

store/update max during in-order traversal.
return maximum branches
a) 0
b)root.val
c)root.val + dfs(root.left)
d) root.val + dfs(root.right)
Whole situation can be broken down to four cases:

root
left<0 right<0
max = Math.max(0, root.val + 0 + 0), return Math.max(0,root.val)
root
left>0 right<0
max = Math.max(0, root.val + dfs(root.left) + 0), return Math.max(0, root.val + dfs(root.left))
root
left<0 right>0
max = Math.max(0, root.val + 0+ dfs(root.right) + 0), return Math.max(0, root.val + dfs(root.right))
4)root
left>0 right>0
max = Math.max(0, root.val + 0+ dfs(root.left) + dfs(root.right) ), return Math.max(0, root.val + dfs(root.left) + dfs(root.right))
```

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    ans = float("-inf")
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """

        self.dfs(root)
        return self.ans
    def dfs(self,root):
        if not root:
            return 0
        left = max(0,self.dfs(root.left))
        right = max(0,self.dfs(root.right))
        self.ans = max(self.ans,left+right+root.val)
        return max(0,left+root.val,right+root.val)
```

