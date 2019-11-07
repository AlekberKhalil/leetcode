# reverse linked list II

Reverse a linked list from positionmton. Do it in-place and in one-pass.

For example:  
Given`1->2->3->4->5->NULL`,m= 2 andn= 4,

return`1->4->3->2->5->NULL`.

**Note:**  
Givenm,nsatisfy the following condition:  
1 ≤m≤n≤ length of list.

分析

2种reverse方法，一种只改变中间指针指向，还有一种不断把next插入prev的后面，头插法？也是循环首位相接

```text
ListNode temp = cur.next;cur.next = prev;prev = cur;cur = temp;
```

```text
头插法？不断把cur后面的Node插入prev的后面ListNode move = cur.next;cur.next = move.next;move.next = prev.next;prev.next = move;
```

此题从dummy开始，走m-1步到m前，然后开始头插法把后面的数不断插入m-1之后。

```text
/** * Definition for singly-linked list. * public class ListNode { *     int val; *     ListNode next; *     ListNode(int x) { val = x; } * } */class Solution {    public ListNode reverseBetween(ListNode head, int m, int n) {        ListNode dummy = new ListNode(0);        dummy.next = head;        ListNode prev = dummy, cur;        for(int i = 0; i < m - 1; i ++){            if(prev != null)                prev = prev.next;        }        cur = prev.next;        for(int i = m; i < n; i ++){            ListNode move = cur.next;            cur.next = move.next;            move.next = prev.next;            prev.next = move;        }        return dummy.next;    }}
```

