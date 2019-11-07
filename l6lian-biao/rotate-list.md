# rotate list

Given a list, rotate the list to the right bykplaces, wherekis non-negative.

For example:  
Given`1->2->3->4->5->NULL`andk=`2`,  
return`4->5->1->2->3->NULL`.

分析

这里k要k%len，

* 用首位相连，然后头部走len-k就断开。
* 我的做法是两指针，一个指针先走k步，然后两个指针一起走。快指针到尾部，慢指针可以断开了。

计算链表长度：

* 从dummy 开始，走到最后一个，即p.next != null
* 从head开始，走到null，p != null

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
    public ListNode rotateRight(ListNode head, int k) {        
        if(head == null || head.next == null){
            return head;
        }
        int len = 0;
        ListNode p = head;
        while(p != null){
            p = p.next;
            len++;
        }
        k = k % len;
        if(k == 0)
            return head;

        ListNode h1 = head;
        ListNode prev = head;

        for(int i = 0; i < k; i ++){
            if(prev != null)
                prev = prev.next;
        }
        while(prev!=null && prev.next != null){
            head = head.next;
            prev = prev.next;
        }
        p = head;
        head = head.next;
        p.next = null;
        if(prev != null)
            prev.next = h1;
        return head;

    }
}
```

