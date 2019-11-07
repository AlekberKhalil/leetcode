# Average of Levels in Binary Tree\(BFS Tree\)

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**

```text
Input:    3   / \  9  20    /  \   15   7Output: [3, 14.5, 11]Explanation:The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

分析

bfs tree

```text
# Definition for a binary tree node.# class TreeNode:#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass Solution:    def averageOfLevels(self, root):        """        :type root: TreeNode        :rtype: List[float]        """        q = collections.deque()        q.append(root)        ret = []        while q:            l = len(q)            sum = 0            for i in range(l):                cur = q.popleft()                sum += cur.val                if cur.left:                    q.append(cur.left)                if cur.right:                    q.append(cur.right)            ret.append(sum/l)        return ret
```

