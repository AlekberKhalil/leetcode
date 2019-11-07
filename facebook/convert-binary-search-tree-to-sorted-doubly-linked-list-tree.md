# Convert Binary Search Tree to Sorted Doubly Linked List  （Tree\)

Convert a BST to a sorted circular doubly-linked list in-place. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.

> ![](http://4.bp.blogspot.com/_UElib2WLeDE/TPRo1mUmf2I/AAAAAAAACZM/BzwriSAGybw/s1600/tree.png)
>
> ![](http://4.bp.blogspot.com/_UElib2WLeDE/TPRo9cJLq_I/AAAAAAAACZQ/aiBIfOyQFX0/s1600/treelist2.gif)

![](http://1.bp.blogspot.com/_UElib2WLeDE/TPR8ILKoieI/AAAAAAAACZY/BoU90YXHePc/s1600/doublylist.gif)

A circular doubly-linked list. Think of the left and right pointers in a tree as synonymous to the previous and next pointers in a list.

The idea is using in-order traversal set previous visited node's left node points to current node, and current node's right node points to previous visited node.

How do we set head's left points to last and the last's right points to head? We just need to keep the head node and let it's left points to the current node, and current node's right points to the head node.

edge case: root node only, we need to point left and right to root itself.

分析

就是树的Inorder 加上prev cur之类的指针

```text
from TreeNode import TreeNodeclass Solution:    def bstToSortedDLL(self,root):        head = TreeNode(-1)        head.right = root        stack = []        cur,prev = root,None        first = True        while cur or stack:            while cur:                stack.append(cur)                cur = cur.left            cur = stack.pop()            if first:                head.right = cur                first = False            if prev:                prev.right = cur                cur.left = prev            prev = cur            cur = cur.right        if prev:            prev.right = head.right            head.right.left = prev        return head    def print_list(self,head):        """Function to print the given           doubly linked list"""        if head is None:            return        while head:            print(head.val)            head = head.rightroot = TreeNode(10)root.left = TreeNode(12)root.right = TreeNode(15)root.left.left = TreeNode(25)root.left.right = TreeNode(30)root.right.left = TreeNode(36)obj = Solution()head = obj.bstToSortedDLL(root)obj.print_list(head)
```

recursive：这里最后的prev就是最后的node,和head串起来就行了

```text
    head = prev =  None    def bstToSortedDLLRe(self, root):        if not root:            return        self.bstToSortedDLLRe(root.left)        if not self.prev:            self.head = root        else:            self.prev.right = root            root.left = self.prev        self.prev = root        self.bstToSortedDLLRe(root.right)    def helper(self,root):        self.bstToSortedDLLRe(root)        self.prev.right = self.head        self.head.left = self.prev
```

