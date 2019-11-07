# Sum Root to Leaf Numbers\(recrusive\)

Given a binary tree containing digits from`0-9`only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path`1->2->3`which represents the number`123`.

Find the total sum of all root-to-leaf numbers.

**Note:** A leaf is a node with no children.

**Example:**

```text
Input: [1,2,3]    1   / \  2   3Output: 25Explanation:The root-to-leaf path 1->2 represents the number 12.The root-to-leaf path 1->3 represents the number 13.Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

```text
Input: [4,9,0,5,1]    4   / \  9   0 / \5   1Output: 1026Explanation:The root-to-leaf path 4->9->5 represents the number 495.The root-to-leaf path 4->9->1 represents the number 491.The root-to-leaf path 4->0 represents the number 40.Therefore, sum = 495 + 491 + 40 = 1026.
```

分析

叶子只负责算Pathsum。root只负责把左右相加。值得注意的做法

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def sumNumbers(self, root):        """        :type root: TreeNode        :rtype: int        """        return self.dfs(root,0)    def dfs(self,root,pathsum):        if not root:            return 0        #leaf get pathsum        if not root.left and not root.right:            return root.val+pathsum*10        #root only calculate        return self.dfs(root.left, pathsum*10+root.val)+self.dfs(root.right, pathsum*10+root.val)
```

