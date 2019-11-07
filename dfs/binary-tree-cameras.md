# Binary Tree Cameras

Given a binary tree, we install cameras on the nodes of the tree.

Each camera at a node can monitor**its parent, itself, and its immediate children**.

Calculate the minimum number of cameras needed to monitor all nodes of the tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_01.png)

```text
Input: [0,0,null,0,0]Output: 1Explanation: One camera is enough to monitor all nodes if placed as shown.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/29/bst_cameras_02.png)

```text
Input: [0,0,null,0,null,0,null,null,0]Output: 2Explanation: At least two cameras are needed to monitor all nodes of the tree. The above image shows one of the valid configurations of camera placement.
```

Note:

```text
The number of nodes in the given tree will be in the range [1, 1000].Every node has value 0.
```

分析

3个状态NOT\_MONITORED = 0

```text
    MONITORED\_NOCAM = 1    MONITORED\_WITHCAM = 2
```

尽量往上放

1 2个儿子都被监视，求助parent

2任意儿子不被监视，本地放置 res++

3 直接返回被监视（可能儿子处放置

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def minCameraCover(self, root: TreeNode) -> int:        NOT_MONITORED = 0        MONITORED_NOCAM = 1        MONITORED_WITHCAM = 2        cameras = 0        if not root:                return 0        def dfs(root: TreeNode) -> int:            nonlocal cameras            if not root:                return MONITORED_NOCAM            left = dfs(root.left)            right = dfs(root.right)            if left == MONITORED_NOCAM and right ==MONITORED_NOCAM:                 return NOT_MONITORED            elif left == NOT_MONITORED or right == NOT_MONITORED:                cameras += 1                return MONITORED_WITHCAM                        else:                return MONITORED_NOCAM        top = dfs(root)        return cameras+1 if  top== NOT_MONITORED else cameras
```

