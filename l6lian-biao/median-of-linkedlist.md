# Median of LinkedList

输出单链表的中位数

分析

快慢都从头，快到尾，慢指针在中间或者偏后

len从1开始，每次+2，最后如果快指针是空，记得-1

```text
class ListNode:    def __init__(self,val):        self.val = val        self.next = Noneclass Solution:    def middleOfLinkedList(self,l):        if not l or not l.next:            return l        slow = quick = l        pre = None        n = 1        while quick and quick.next:            n += 2            pre = slow            slow = slow.next            quick = quick.next.next        if not quick:            n -= 1        if n % 2 == 0:            return (pre.val + slow.val) /2        else:            return slow.vall2 = ListNode(1)l2.next = ListNode(2)l2.next.next = ListNode(4)l2.next.next.next = ListNode(5)l2.next.next.next.next = ListNode(9)l2.next.next.next.next.next = ListNode(11)s = Solution()res = s.middleOfLinkedList(l2)print(res)
```

