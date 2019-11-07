# Merge k sorted list

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

分析

K路归并，用priority queue, 注意loop array时候，null的element不要加入queue

```text
public ListNode mergeKLists(ListNode[] lists) {        if(lists == null || lists.length == 0)            return null;        int k = lists.length;        Queue<ListNode> q = new PriorityQueue<ListNode>(k, new Comparator<ListNode>(){            public int compare(ListNode a, ListNode b){                return a.val - b.val;            }        });        for(ListNode e : lists){            if(e != null)                q.offer(e);        }        ListNode dummy = new ListNode(0);        ListNode cur = dummy;        while(!q.isEmpty()){            cur = cur.next = q.poll();            if(cur != null && cur.next != null){                q.offer(cur.next);            }        }        return dummy.next;    }
```

python, 用tuple塞入heapq \(node.val,node\)

```text
# Definition for singly-linked list.# class ListNode(object):#     def __init__(self, x):#         self.val = x#         self.next = Noneclass Solution(object):    def mergeKLists(self, lists):        """        :type lists: List[ListNode]        :rtype: ListNode        """        dummy = ListNode(-1)        prev = dummy        pq = []        for i in lists:            if i:                heapq.heappush(pq,(i.val,i))        while pq:            cur = heapq.heappop(pq)[1]            prev.next = cur            prev = cur            if cur.next:                heapq.heappush(pq,(cur.next.val,cur.next))        return dummy.next
```

必须塞入list的index入tuple,防止value相同时候

```text
# Definition for singly-linked list.# class ListNode:#     def __init__(self, x):#         self.val = x#         self.next = Noneclass Solution:    def mergeKLists(self, lists: List[ListNode]) -> ListNode:               res = ListNode(-1)        q = [(n.val, i,n) for i,n in enumerate(lists) if n]        heapq.heapify(q)        cur = res        while q:            v,i,node = heapq.heappop(q)            cur.next = node            cur = node            if cur.next:                heapq.heappush(q, (cur.next.val,i,cur.next)) #val可能一样，用i代表来自哪个数组。。  。        return res.next                                
```

