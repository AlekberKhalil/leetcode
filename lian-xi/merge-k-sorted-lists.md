# Merge k Sorted Lists

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

分析

1.判断lists是否为空

1. PriorityQueue 有类不是Linkedlist，同时类型是Queue也不是Heap

```text
2.Queue<ListNode> minHeap = new PriorityQueue<ListNode>(size, Comparator)
```

3.Comparator 的compare函数必须是public!!!!!

4.PriorityQueue的函数offer poll isEmpty\(\)

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        Queue<ListNode> minHeap = new PriorityQueue<ListNode>(lists.length, new Comparator<ListNode>(){
            public int compare(ListNode l1, ListNode l2){
                return l1.val - l2.val;
            }
        });

        ListNode dummy = new ListNode(0); 
        ListNode prev = dummy;
        for(ListNode l : lists){
            if(l != null){
                minHeap.offer(l);
            }
        }

        while(!minHeap.isEmpty()){
            ListNode cur = minHeap.poll();
            prev.next = cur;
            prev = prev.next;
            if(cur.next != null)
                minHeap.offer(cur.next);
        }

        return dummy.next;
    }
}
```

