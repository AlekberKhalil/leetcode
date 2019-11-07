# Binary Search Tree Iterator\(tree inorder\)

Implement an iterator over a binary search tree \(BST\). Your iterator will be initialized with the root node of a BST.

Calling`next()`will return the next smallest number in the BST.

**Note:**`next()`and`hasNext()`should run in average O\(1\) time and uses O\(h\) memory, wherehis the height of the tree.

分析

inorder

iterative: **hasnext里是while的条件** next里是遍历的过程。要拆开。想象不断调用hasnext 就是不断while

recursive的话就是直接Inorder做完存在List里。然后控制List的index

follow up: post order，一样遍历，就是捕捉stack pop的瞬间

```text
# Definition for a  binary tree node# class TreeNode(object):#     def __init__(self, x):#         self.val = x#         self.left = None#         self.right = Noneclass BSTIterator(object):    def __init__(self, root):        """        :type root: TreeNode        """        self.stack = []        self.cur = root    def hasNext(self):        """        :rtype: bool        """        return self.cur or self.stack    def next(self):        """        :rtype: int        """        while self.cur:            self.stack.append(self.cur)            self.cur = self.cur.left        res = self.stack.pop()        self.cur = res.right        return res.val# Your BSTIterator will be called like this:# i, v = BSTIterator(root), []# while i.hasNext(): v.append(i.next())
```

