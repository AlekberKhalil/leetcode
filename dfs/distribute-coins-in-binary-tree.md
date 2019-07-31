# Distribute Coins in Binary Tree

Given the`root`of a binary tree with`N`nodes, each`node` in the tree has`node.val`coins, and there are`N`coins total.

In one move, we may choose two adjacent nodes and move one coin from one node to another. \(The move may be from parent to child, or from child to parent.\)

Return the number of moves required to make every node have exactly one coin.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/18/tree1.png)

```text
Input: 
[3,0,0]
Output: 
2
Explanation: 
From the root of the tree, we move one coin to its left child, and one coin to its right child.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/01/18/tree2.png)

```text
Input: 
[0,3,0]
Output: 
3
Explanation: 
From the left child of the root, we move two coins to the root [taking two moves].  Then, we move one coin from the root of the tree to the right child.
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/01/18/tree3.png)

```text
Input: 
[1,0,2]
Output: 
2
```

**Example 4:**

![](https://assets.leetcode.com/uploads/2019/01/18/tree4.png)

```text
Input: 
[1,0,0,null,3]
Output: 
4
```

**Note:**

```text
1<= N <= 100
0 <= node.val <= N
```

分析

Recursive method is indeed to find needed coins in a bottom-up way.

1. If the node is null, it require no coins.
2. If the node does't have enough coins to feed its children and itself \(require n\), it need to ask n coins from its parent. So

   `count = count + n`

3. If the node have extra coins to feed its children and itself \(extra n\), it need to pass n coins from its parent. So

   `count = count + n`

![image](https://assets.leetcode.com/users/votrubac/image_1548011422.png)

直接改原函数和node val. If we can modify values of tree nodes, we can store the balance in nodes, and use the return value to accumulate the number of moves. This way we can get rid of the helper method. 原函数同时处理父节点 pre,子节点，和自己。父节点就是+=root.val-1。自己的值就是左右+self-1返回用。结果是左右+self的abs。这里root.val可以是负数，move是abs

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def distributeCoins(self, root: TreeNode,pre = None) -> int:
        if not root:
            return 0
        res = self.distributeCoins(root.left,root)+self.distributeCoins(root.right,root)
        if pre:
            pre.val += root.val - 1
        return res + abs(root.val - 1)
```

DFS

好理解版本：[https://leetcode.com/problems/distribute-coins-in-binary-tree/discuss/222000/A-better-illustration-of-recursive-method](https://leetcode.com/problems/distribute-coins-in-binary-tree/discuss/222000/A-better-illustration-of-recursive-method)

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def distributeCoins(self, root: TreeNode) -> int:
        res = 0
        def helper(root):
            nonlocal res
            if not root:
                return 0
            left = helper(root.left)
            right = helper(root.right)            

            res += abs(left)+abs(right)

            return left+right+root.val - 1
        helper(root)
        return res
```

