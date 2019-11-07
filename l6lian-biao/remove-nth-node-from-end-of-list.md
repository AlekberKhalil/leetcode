# Remove Nth Node From End of List

```text
Given a linked list, remove the nth node from the end of list and return its head.For example,   Given linked list: 1->2->3->4->5, and n = 2.   After removing the second node from the end, the linked list becomes 1->2->3->5.Note:Given n will always be valid.Try to do this in one pass.
```

分析

两个指针，一个先前进n，然后另一个一起移动，直到第一个达到尾部。

**这题非要2个指针都从dummy起，从Head起就是不行，虽然做法完全一样。**

**因为可能删除的是头结点，所以一定要从dummy起。**

```text
/** * Definition for singly-linked list. * public class ListNode { *     int val; *     ListNode next; *     ListNode(int x) { val = x; } * } */class Solution {    public ListNode removeNthFromEnd(ListNode head, int n) {                ListNode dummy = new ListNode(0);        dummy.next = head;        ListNode quick = dummy, slow = dummy;        for(int i = 0; i <= n; i++){            quick = quick.next;        }        while(quick != null){                       slow = slow.next;            quick = quick.next;        }            slow.next = slow.next.next;        return dummy.next;    }}
```

