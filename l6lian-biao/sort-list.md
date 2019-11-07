# sort list

Sort a linked list inO\(nlogn\) time using constant space complexity.

分析

分治法，注意分治法和快排的区别。分治时只要中部分开即可，merge时候会有大小判断。快排需要用pivot把大小区别开来。

用快慢指针找到中部位置。偶数时slow靠后，用prev。不要忘了前半list末尾置为0

```text
/** * Definition for singly-linked list. * public class ListNode { *     int val; *     ListNode next; *     ListNode(int x) { val = x; } * } */class Solution {    public ListNode sortList(ListNode head) {        if (head == null || head.next == null)//排除空和一个元素的情况            return head;        ListNode prev = null, slow = head, quick = head;//prev需要初始化        while(quick != null && quick.next != null){            prev = slow;//偶数时候slow在偏后，所以用prev来表示slow前位置            slow = slow.next;            quick = quick.next.next;        }        prev.next = null;//前半list末尾置为0        ListNode l1 = sortList(head);        ListNode l2 = sortList(slow);        ListNode l3 = merge(l1, l2);        return l3;    }    ListNode merge(ListNode l1, ListNode l2){        ListNode dummy = new ListNode(0);        ListNode cur = dummy;        while(l1 != null && l2 != null){            if(l1.val < l2.val){                cur.next = l1;                l1 = l1.next;            }else{                cur.next = l2;                l2 = l2.next;            }            cur = cur.next;        }        cur.next = l1 != null ? l1 : l2;        return dummy.next;    }}
```

