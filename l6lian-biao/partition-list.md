# partition list

Given a linked list and a valuex, partition it such that all nodes less thanxcome before nodes greater than or equal tox.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,  
Given`1->4->3->2->5->2`andx= 3,  
return`1->2->2->4->3->5`.

分析

4个指针，2个左右dummy，2个指向他们的指针。

最后右指针结尾一定要置空！！！

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
    public ListNode partition(ListNode head, int x) {
        ListNode left = new ListNode(0);
        ListNode right = new ListNode(0);
        ListNode p1 = left, p2 = right;
        while(head != null){
            if(head.val < x){
                p1.next = head; //p1 = p1.next = head;
                p1 = head;
            }else{
                p2.next = head; //p2 = p2.next = head;
                p2 = head;
            }
            head = head.next;
        }

        p1.next = right.next;
        p2.next = null;//缺了这一步，一定要把右指针结尾置空！！！！！
        return left.next;
    }
}
```

