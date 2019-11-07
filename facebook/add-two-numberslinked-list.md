# Add Two Numbers\(linked list\)

You are given two**non-empty**linked lists representing two non-negative integers. The digits are stored in**reverse order**and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```text
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)Output: 7 -> 0 -> 8Explanation: 342 + 465 = 807.
```

分析

while l1 or l2 or carry:包含所有情况，记得cur l1 l2都要往下走

```text
# Definition for singly-linked list.# class ListNode:#     def __init__(self, x):#         self.val = x#         self.next = Noneclass Solution:    def addTwoNumbers(self, l1, l2):        """        :type l1: ListNode        :type l2: ListNode        :rtype: ListNode        """        carry = 0        dummy = ret = ListNode(-1)        while l1 or l2 or carry:            if l1:                carry += l1.val                l1 = l1.next            if l2:                carry += l2.val                l2 = l2.next            ret.next = ListNode(carry%10)            ret = ret.next            carry //= 10         return dummy.next
```

