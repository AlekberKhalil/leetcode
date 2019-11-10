# remove duplicates from sorted list II

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only _distinct_ numbers from the original list.

分析

比较cur和cur.next，删除当前节点cur，不动prev，否则移动prev。注意有个continue,处理连续不同dup的情况。

```text
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        boolean hasDup = false;
        ListNode prev = dummy, cur = head;
        while(cur != null){
            hasDup = false;
            while(cur != null && cur.next != null && cur.val == cur.next.val){
                hasDup = true;
                cur = cur.next;
                prev.next = cur;  
            }

            if(hasDup){
                cur = cur.next;
                prev.next = cur;  
                continue;//缺了这一行！！！
            }

            if(cur != null){
                prev = prev.next;
                cur = cur.next;              
            }

        }

        return dummy.next;
    }
}
```

