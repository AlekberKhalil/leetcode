# Sort List



Sort a linked list in _O_\(_n_ log _n_\) time using constant space complexity.

**Example 1:**

```text
Input: 4->2->1->3
Output: 1->2->3->4
```

**Example 2:**

```text
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

\*\*\*\*

**分析**

**mergesort 注意快慢指针结束，slow在中偏后**

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        slow = quick = head        
        pre = None
        while quick and quick.next:
            pre = slow
            slow = slow.next
            quick = quick.next.next
           
        
        pre.next = None        
        lh = self.sortList(head)
        rh = self.sortList(slow)
        
        p = res = ListNode(-1)
        
        while lh and rh:
            if lh.val < rh.val:
                res.next = lh
                lh = lh.next
            else:
                res.next = rh
                rh = rh.next
            res = res.next
        if lh:
            res.next = lh
        if rh:
            res.next = rh      
        
        return p.next
        
        
        
        
        
```

**recursive**

```text
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        slow = quick = head        
        pre = None
        while quick and quick.next:
            pre = slow
            slow = slow.next
            quick = quick.next.next
           
        
        pre.next = None        
        lh = self.sortList(head)
        rh = self.sortList(slow)
        
        def merge(l,r):
            if not l:
                return r
            if not r:
                return l
            res = None
            
            if l.val < r.val:
                res = l
                res.next = merge(l.next,r)
            else:
                res = r
                res.next = merge(l,r.next)
            return res
        
                    
        
        return merge(lh,rh)
        
        
        
        
        
        
```

