# Reverse Nodes in k-Group\(linkedlist\)

Given a linked list, reverse the nodes of a linked list\_k\_at a time and return its modified list.

\_k\_is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of\_k\_then left-out nodes in the end should remain as it is.

* **Example:**

```text
Given this linked list: 1->2->3->4->5For k = 2, you should return: 2->1->4->3->5For k = 3, you should return: 3->2->1->4->5
```

分析

每个group里cur 和next翻转，记得只要翻k-1次，pre不要动. 翻完以后 利用pre要和前后group连接。设置好pre的next，是为了结果返回对的header

helper函数返回的是最后一个node，好作为将来下一个group的pre

```text
# Definition for singly-linked list.# class ListNode:#     def __init__(self, x):#         self.val = x#         self.next = Noneclass Solution:    def reverseKGroup(self, head, k):        """        :type head: ListNode        :type k: int        :rtype: ListNode        """        n = 0        dummy = ListNode(-1)        dummy.next = head        cur = head        while cur:            n += 1            cur = cur.next        q = dummy        for i in range(n // k):            q = self.helper(q, k)#q是前group的最后一个Node        return dummy.next    def helper(self, pre, k):        if not pre or not pre.next:            return None        cur = pre.next        nxt = cur.next        #prev不参与，只翻转cur 和 next        for i in range(1, k): #1开始是因为5个元素翻转，只需要翻转4次            nnxt = nxt.next            nxt.next = cur            cur = nxt            nxt = nnxt        #这步很重要 把本group和前面prev 后面nxt连起来，同时pre指向新头        temp = pre.next        pre.next.next = nxt        pre.next = cur #pre指向新头,是为了最后的结果dummy返回头        return temp
```

