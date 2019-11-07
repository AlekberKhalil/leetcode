# All Nodes Distance K in Binary Tree

```text
We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.



Example 1:

Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation: 
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.



Note that the inputs "root" and "target" are actually TreeNodes.
The descriptions of the inputs above are just serializations of these objects.


Note:

The given tree is non-empty.
Each node in the tree has unique values 0 <= node.val <= 500.
The target node is a node in the tree.
0 <= K <= 1000.
```

分析

DFS把父子相连，都放入对方的List

bfs从target开始走K层

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def distanceK(self, root, target, K):
        """
        :type root: TreeNode
        :type target: TreeNode
        :type K: int
        :rtype: List[int]
        """
        m = collections.defaultdict(list)
        def dfs(root):
            if not root:
                return              
            if root.left:
                m[root.val].append(root.left.val)
                m[root.left.val].append(root.val)
                dfs(root.left)
            if root.right:
                m[root.val].append(root.right.val)
                m[root.right.val].append(root.val)
                dfs(root.right)
        dfs(root)
        q = [target.val]
        seen = set(q)
        while K:
            q = [i for j in q for i in m[j] if i not in seen]
            seen |= set(q)
            K -= 1           
        return q
```

