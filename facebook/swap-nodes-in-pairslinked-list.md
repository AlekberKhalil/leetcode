# Swap Nodes in Pairs\(linked list\)

Given a linked list, swap every two adjacent nodes and return its head.

**Example:**

```text
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

分析

prev=dummy， prev之后的cur 和next互换 prev别动。 完了prev=cur cur= cur.next

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = head
        prev = dummy
        cur = head
        while cur and cur.next:
            nxt = cur.next
            cur.next = nxt.next
            nxt.next = prev.next
            prev.next = nxt

            prev = cur
            cur = cur.next
        return dummy.next
```

