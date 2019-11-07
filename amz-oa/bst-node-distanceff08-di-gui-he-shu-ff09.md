# BST Node Distance（递归和树）

## Description

Given a list of numbers, construct a BST from it\(you need to insert nodes one-by-one with the given order to get the BST\) and find the distance between two given nodes.

* If two nodes do not appear in the BST, return

  `-1`

* We guarantee that there are no duplicate nodes in BST
* The node distance means the number of edges between two nodes

Have you met this question in a real interview?

Yes

Problem Correction

## Example

```text
input:numbers = [2,1,3]node1 = 1node2 = 3output:2
```

分析

1.建树，用每个Node insert:注意这里root直接传入的话不会赋值，只能return root才行

2.最近公共parent，LCA然后到parent的dist1+dist2

注意这里超时，所以是在lca里直接得到距离。&gt; root 去右 &lt;root去左，一大一小root是LCA，用getrootdist。

3.getrootdist用递归，注意这里找不到node返回无穷大。这样没有的话&lt;0结果就返回-1

refer to:[https://www.geeksforgeeks.org/shortest-distance-between-two-nodes-in-bst/](https://www.geeksforgeeks.org/shortest-distance-between-two-nodes-in-bst/)

```text
class Solution:    """    @param numbers: the given list    @param node1: the given node1    @param node2: the given node2    @return: the distance between two nodes    """    class TreeNode:        def __init__(self, val):            self.val = val            self.left = None            self.right = None    def bstDistance(self, numbers, node1, node2):        # Write your code here        if not numbers:            return 0        root = None        for ii,i in enumerate(numbers):            if ii == 0:                root = self.insertTree(i,root)            else:                self.insertTree(i, root)        map = {}        return self.getLCA(node1, node2, root, map)    def insertTree(self, i, root):        if root:            if i > root.val:                root.right = self.insertTree(i, root.right)            else:                root.left = self.insertTree(i, root.left)        else:            root = self.TreeNode(i)        return root    def getLCA(self, p, q, root, map):        if (root.val - p) > 0 and (root.val - q) > 0:            return self.getLCA(p, q, root.left, map)        elif (root.val - p) < 0 and (root.val - q) < 0:            return self.getLCA(p, q, root.right, map)        else:            a = self.getrootdist(p, root, map)            b = self.getrootdist(q, root, map)            if a >= 0 and b >= 0:                return a + b            else:                return -1    def getrootdist(self, i, root, map):        res = None        if i in map:            return map[i]        if not root:            return float('-inf')        if root.val == i:            return 0        elif root.val < i:            res = 1 + self.getrootdist(i, root.right, map)        else:            res = 1 + self.getrootdist(i, root.left, map)            map[i] = res        return res
```

