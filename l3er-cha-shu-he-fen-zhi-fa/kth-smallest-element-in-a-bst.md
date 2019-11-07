# Kth Smallest Element in a BST

Given a binary search tree, write a function`kthSmallest`to find the**k**th smallest element in it.

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Example 1:**

```text
Input: root = [3,1,4,null,2], k = 1   3  / \ 1   4  \   2Output: 1
```

**Example 2:**

```text
Input: root = [5,3,6,2,4,null,null,1], k = 3       5      / \     3   6    / \   2   4  / 1Output: 3
```

**Follow up:**  
What if the BST is modified \(insert/delete operations\) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

分析

中序遍历，记得这里k和res都要Nonlocal

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def kthSmallest(self, root: TreeNode, k: int) -> int:                 res = None        def helper(root):            nonlocal res,k            # if not root:            #     return            if root.left:                helper(root.left)            k -= 1            if k == 0 :                res = root.val                return            if root.right:                helper(root.right)        helper(root)        return res
```

iterative

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def kthSmallest(self, root: TreeNode, k: int) -> int:        stack = []        cur = root        while cur or stack: #错在Not stack...            while cur:                stack.append(cur)                cur = cur.left            cur = stack.pop()            k -= 1            if not k:                return cur.val            cur = cur.right
```

