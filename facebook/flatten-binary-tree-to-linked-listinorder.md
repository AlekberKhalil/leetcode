# Flatten Binary Tree to Linked List\(inorder\)

Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

```text
    1
   / \
  2   5
 / \   \
3   4   6
```

The flattened tree should look like:

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

分析

题目是preorder我做的是双链表Inorder

注意Inorder赋right时候，没有right才赋值，有的话别动！！！

```text
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        stack=[]
        cur = root
        head=TreeNode(-1)
        First = 1
        prev=None
        while cur or stack:
            while cur:
                stack.append(cur)
                cur = cur.left
            p=stack.pop()

            if First:
                head = p
                First =0
            cur = p.right
            p.left = prev
            if not p.right and stack:
                p.right = stack[-1]
            prev = p

        ret = head
        # while ret:
        #     print(ret.val)
        #     ret = ret.right
        while prev:
            print(prev.val)
            prev = prev.left
```

