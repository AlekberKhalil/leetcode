# Plus One Linked List



Given a non-negative integer represented as **non-empty** a singly linked list of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

**Example :**

```text
Input: [1,2,3]
Output: [1,2,4]
```

分析

iterative 最后一个非9 + 1，后面9都设置为0，dummy.next = head dummy指针判断后返回

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        if not head:
            return ListNode(1)
        
        dummy=lastnonine = ListNode(0)
        dummy.next = head
        p=head
        while p:
            if p.val!=9:
                lastnonine = p
            p = p.next

        lastnonine.val += 1
        p = lastnonine.next
        while p:
            p.val = 0
            p=p.next
        return dummy if dummy.val != 0 else dummy.next

```

dfs,返回carry

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        def helper(head):
            if not head:
                return 1 #1不是0
            carry = helper(head.next)
            if not carry:
                return 0
            x = head.val + 1
            head.val = x%10 #注意相反
            return x//10
        
        if not helper(head):
            return head
        node = ListNode(1)
        node.next = head
        return node
```

return node, 直接原函数做， 返回的不是Head就是新加头

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        if not head:
            return ListNode(1)
        nxt = self.plusOne(head.next)
        if head.next != nxt:
            head.val += 1
        if head.val <= 9:
            return head
        head.val = 0
        node = ListNode(1)
        node.next = head
        return node
        
```

