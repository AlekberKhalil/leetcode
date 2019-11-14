# Convert Sorted List to Binary Search Tree



Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of _every_ node never differ by more than 1.

**Example:**

```text
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```



分析

快慢指针到中间，head左边 slow右边，记得pre后断开链表

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        if not head:
            return None
        if not head.next:
            return TreeNode(head.val)
        slow = quick = head
        pre = None
        while quick and quick.next:
            pre = slow
            slow = slow.next
            quick = quick.next.next
        root = TreeNode(slow.val)
        pre.next = None
        root.right = self.sortedListToBST(slow.next)
        root.left =  self.sortedListToBST(head)
        return root
        
        
```



