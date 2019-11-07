# Palindrome Linked List\(linked list\)

Given a singly linked list, determine if it is a palindrome.

```text
Given a singly linked list, determine if it is a palindrome.

Example 1:

Input: 1->2
Output: false
Example 2:

Input: 1->2->2->1
Output: true
Follow up:
Could you do it in O(n) time and O(1) space?
```

**Follow up:**  
Could you do it in O\(n\) time and O\(1\) space?

分析：

快慢指针。通从head出发，quick为空，slow在中后部，记得返回pre-mid

reverse的时候，返回prev就是新head

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """

        if not head or not head.next:
            return True
        head1=head
        premid=self.getMid(head1)
        rList = self.reverse(premid.next)
        premid.next = None
        while head and rList:
            if head.val != rList.val:
                return False
            head = head.next
            rList = rList.next
        return True


    def getMid(self,head):
        prev=slow=quick=head
        while quick and quick.next:
            prev = slow
            slow = slow.next
            quick =quick.next.next
        return prev

    def reverse(self,head):
        prev = ListNode(-1)
        prev.next = head

        while head:
            nxt = head.next
            head.next = prev
            prev = head
            head=nxt
        return prev
```

