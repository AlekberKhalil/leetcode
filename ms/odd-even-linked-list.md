# Odd Even Linked List



Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O\(1\) space complexity and O\(nodes\) time complexity.

**Example 1:**

```text
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
```

**Example 2:**

```text
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

**Note:**

* The relative order inside both the even and odd groups should remain as it was in the input.
* The first node is considered odd, the second node even and so on

分析

快指针做法，初始指向奇偶数头

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        eh = ep = p = head
        oh = op = q =head.next
        while ep and ep.next and op and op.next:
            ep = ep.next.next
            op = op.next.next
            eh.next = ep
            eh = eh.next
            oh.next = op
            oh = oh.next
        eh.next = q
        return p
```

