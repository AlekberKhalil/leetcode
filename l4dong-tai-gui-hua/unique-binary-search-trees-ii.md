# Unique Binary Search Trees II

Given an integer_n_, generate all structurally unique**BST's**\(binary search trees\) that store values 1 ... _n_.

**Example:**

```text
Input: 3Output:[  [1,null,3,2],  [3,2,null,1],  [3,1,null,null,2],  [2,1,3],  [1,null,2,null,3]]Explanation:The above output corresponds to the 5 unique BST's shown below:   1         3     3      2      1    \       /     /      / \      \     3     2     1      1   3      2    /     /       \                 \   2     1         2                 3
```

分析

范围内建树min和max

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def generateTrees(self, n: int) -> List[TreeNode]:             if not n:            return []        def helper(mn,mx):            if mn>mx:                return [None]            if mn == mx:                return [TreeNode(mn)]            res = []            for i in range(mn,mx+1):                                for l in helper(mn,i-1):                    for r in helper(i+1,mx):                        root = TreeNode(i)                        root.left,root.right = l,r                        res.append(root)            return res        return helper(1,n)
```

