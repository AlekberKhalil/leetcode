# copy list with random pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

分析

2个loop，第一个复制新Node插入旧node后面。第二次设置新建Node们的random指针。最后split2个链表

```text
/** * Definition for singly-linked list with a random pointer. * class RandomListNode { *     int label; *     RandomListNode next, random; *     RandomListNode(int x) { this.label = x; } * }; */public class Solution {    public RandomListNode copyRandomList(RandomListNode head) {        RandomListNode dummy = new RandomListNode(0);        dummy.next = head;        RandomListNode cur = head;        while(cur != null){            RandomListNode node = new RandomListNode(cur.label);            node.next = cur.next;            cur.next = node;            cur = node.next;        }        cur = head;        while(cur != null){            if(cur.random != null)//这个不能放在while判断里                cur.next.random = cur.random.next;            cur = cur.next.next;        }        //split        RandomListNode nh = new RandomListNode(0);        cur = nh;        while(head != null){            nh.next = head.next;              nh = nh.next;            head.next = nh.next;                        head = head.next;        }        return cur.next;    }}
```

可以用Map，就是耗空间。用原地copy省空间 No extra space

这里cur=head，用cur走

最后split，cur=dummy=nhead

最后split用cur.next.next一直出错 以后尽量不用.next.next

```text
# Definition for singly-linked list with a random pointer.# class RandomListNode(object):#     def __init__(self, x):#         self.label = x#         self.next = None#         self.random = Noneclass Solution(object):    def copyRandomList(self, head):        """        :type head: RandomListNode        :rtype: RandomListNode        """        if not head:            return head        cur = head        while cur:            copied = RandomListNode(cur.label)            copied.next = cur.next            cur.next = copied            cur = cur.next.next        cur = head        while cur:            if cur.random:                cur.next.random = cur.random.next            cur = cur.next.next        nhead = RandomListNode(-1)        cur = nhead        while head:            nhead.next = head.next            nhead = nhead.next            head.next = nhead.next            head = head.next        return cur.next
```

