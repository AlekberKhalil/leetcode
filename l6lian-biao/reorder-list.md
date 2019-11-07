# reorder list

Given a singly linked listL:L0→L1→…→Ln-1→Ln,  
reorder it to:L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

For example,  
Given`{1,2,3,4}`, reorder it to`{1,4,2,3}`.

分析

快慢指针找到中部分开。然后后半部分用简单reverser，prev设为null!!!

最后2个Merge

```text
/** * Definition for singly-linked list. * public class ListNode { *     int val; *     ListNode next; *     ListNode(int x) { val = x; } * } */class Solution {    public void reorderList(ListNode head) {        if(head == null || head.next == null)            return ;        ListNode prev = null, slow = head, quick = head;        while(quick != null && quick.next != null){            prev = slow;            slow = slow.next;            quick = quick.next.next;        }        prev.next = null;        ListNode  l1 = reverse(slow);        int index = 0;        ListNode cur = new ListNode(0);        while(head != null && l1 != null){            if(index % 2 == 0){                cur.next = head;                head = head.next;            }else{                cur.next = l1;                l1  = l1.next;            }            cur = cur.next;            index++;        }        cur.next = head != null ?  head : l1;        //while可替代                // while(head != null){        //     ListNode n1 = head.next;        //     ListNode n2 = l1.next;        //     head.next = l1;        //     if(n1 == null)        //         break;        //     l1.next = n1;        //     head = n1;        //     l1 = n2;    }    ListNode reverse(ListNode head){        ListNode prev = null;  //很重要！！！              while(head != null){            ListNode temp = head.next;            head.next = prev;            prev = head;            head = temp;        }        return prev;    }}
```

