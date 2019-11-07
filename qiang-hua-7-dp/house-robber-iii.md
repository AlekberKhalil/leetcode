# House Robber III

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```text
Input: [3,2,3,null,3,null,1]3    / \   2   3    \   \ 3   1Output: 7 Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

**Example 2:**

```text
Input: [3,4,5,1,3,null,1]     3    / \45  / \   \  1   3   1Output: 9Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

分析

dfs返回的是【不选，选】

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def rob(self, root):        """        :type root: TreeNode        :rtype: int        """        res = self.helper(root)        return max(res)    def helper(self,root):         # every house you have two option, rob or not rob.         # [value1, value2] value1: not rob current house, rob current house        if not root:            return [0,0]        if not root.left and not root.right:            return [0,root.val]        left = self.helper(root.left)        right = self.helper(root.right)        return [max(left[0],left[1])+max(right[0],right[1]), root.val+left[0]+right[0]]
```

