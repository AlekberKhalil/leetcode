# Data Structure

Queue

可用数据结构：arraylist vector\(cpp\)

Stack

求每个数以它为中心往左/右第一个比它小/大的数 用栈（画图，递增/减的线上以当前点切分为大于/小于的2段）联想二叉树压入栈，左右中关系

计算宽度 y-x-1，中间除x,y外长度

Hash

closed hasing不支持删除操作

hashtable线程安全 但是加锁了，慢。写程序避免用锁

Java hashmap O\(1\)

_**看一个数在不在里面，用Map**_

Heap 堆要填满

Minheap

插入：先加入最底下最左边，一个个网上换 shiftup

删除：也是把用最后那个元素盖住，把该元素移到删除点，然后_**和小的那个儿子换**_（shift up/shit down）

建堆：每个元素Push/pop O（logn）N个数每个数都push pop O（2nlogn\)

比快排,merge sort都慢，空间也大。所以不大用堆排序

实现heap，用数组Array比较好，链表也行

[http://www.cse.hut.fi/en/research/SVG/TRAKLA2/tutorials/heap\_tutorial/taulukkona.html](http://www.cse.hut.fi/en/research/SVG/TRAKLA2/tutorials/heap_tutorial/taulukkona.html)

下标从1开始，0位记载数组的size，则 _left child_: i\*2, _right_ child:i\*2+1， _parent_ i/2

如果顶格开始，从0开始 则_left child_: i\*2+1, _right child_:i\*2+2 _parent ：_\(i-1\)/2

**Priority Queue java implementation**

```text
//priority queuePriorityQueue<int[]> queue = new PriorityQueue<>((a, b) -> (a[0] - b[0]));PriorityQueue<Integer> queue = new PriorityQueue<>(10, Collections.reverseOrder());Queue<ListNode> q = new PriorityQueue<ListNode>(k, new Comparator<ListNode>(){            public int compare(ListNode a, ListNode b){                return a.val - b.val;            }        });//sorthumans.sort((lhs, rhs) -> {    if (lhs.getName().equals(rhs.getName())) {        return lhs.getAge() - rhs.getAge();    } else {        return lhs.getName().compareTo(rhs.getName());    }});humans.sort((h1, h2) -> h1.getName().compareTo(h2.getName()));Collections.sort(edges, new Comparator<Edge>() {            @Override            public int compare(Edge o1, Edge o2) {                if(o1.x!=o2.x){                    return o1.x-o2.x;                }                if(o1.isStart && o2.isStart){                    return o2.height-o1.height;//进入高度从大到小                }                if(!o1.isStart && !o2.isStart){                    return o1.height-o2.height;//出来高度从小到大                }                return o1.isStart ? -1 : 1;//同x，start先end后            }        });//comparatorComparator<int[]> comparator = (e1, e2) -> e1[0] == e2[0] ? e1[1] - e2[1] : e1[0] - e2[0];       Arrays.sort(envelopes, comp);Comparator<Human> comparator = (h1, h2) -> h1.getName().compareTo(h2.getName());class PairComparator implements Comparator<Pair> {    public int compare(Pair a, Pair b) {        return a.val - b.val;    }}
```

