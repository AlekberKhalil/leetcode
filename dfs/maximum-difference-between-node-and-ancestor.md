# Maximum Difference Between Node and Ancestor

Given the`root`of a binary tree, find the maximum value`V`for which there exists**different**nodes`A`and`B`where`V = |A.val - B.val|` and`A`is an ancestor of`B`.

\(A node A is an ancestor of B if either: any child of A is equal to B, or any child of A is an ancestor of B.\)

**Example 1:**

![](http://i68.tinypic.com/2whqcep.jpg)

```text
Input: [8,3,10,1,6,null,14,null,null,4,7,13]Output: 7Explanation: We have various ancestor-node differences, some of which are given below :|8 - 3| = 5|3 - 7| = 4|8 - 1| = 7|10 - 13| = 3Among all possible differences, the maximum value of 7 is obtained by |8 - 1| = 7.
```

**Note:**

```text
The number of nodes in the tree is between 2 and 5000.Each node will have value between 0 and 100000.
```

DFS

一条路上记录最大和最小即可

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def maxAncestorDiff(self, root: TreeNode,mx = float('-inf'),mn= float('inf')) -> int:#         a,b = root.val,root.val#         def dfs(root,mx,mn):            #             if not root:#                 return mx-mn#             mx=max(mx,root.val)#             mn = min(mn,root.val)#             return max(dfs(root.left,mx,mn),dfs(root.right,mx,mn))#         return dfs(root,a,b)        return max(self.maxAncestorDiff(root.left,max(mx,root.val),min(mn,root.val)),self.maxAncestorDiff(root.right,max(mx,root.val),min(mn,root.val))) if root else mx-mn
```

