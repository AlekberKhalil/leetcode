# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

分析

建立dummy和prev，相等，然后prev一个个传下去。

iteration

```text
class Solution {    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {        ListNode dummy = new ListNode(0);        ListNode prev = dummy;        while(l1 != null && l2 != null){            if(l1.val < l2.val){                prev.next = l1;                l1 = l1.next;            }else{                prev.next = l2;                l2 = l2.next;            }            prev = prev.next;        }        if(l1 != null){            prev.next = l1;        }        if(l2 != null){            prev.next = l2;        }        return dummy.next;    }}
```

Recursive

```text
class Solution {    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {        if(l1 == null) return l2;        if(l2 == null) return l1;       if(l1.val < l2.val){           l1.next = mergeTwoLists(l1.next, l2);           return l1;       }else{           l2.next = mergeTwoLists(l1, l2.next);           return l2;       }    }}
```

