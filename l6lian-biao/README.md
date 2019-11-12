# L6\_链表（快慢指针）

必做：

Reverse Nodes in k-Group

reverse:

翻转完头部指针OK，尾部指针需要重设。当前cur就是新头，所以返回头部反而简单。注意初始如果有pre.next = header。那么pre.next指向的是当前尾部，记得利用pre.next设置合适的Next指针。详情见Reverse Nodes in k-Group

reverse linked list,Add Two Numbers II: 先把dummy和cur都相等，然后cur往后走。记得cur先铺好next,然后再跳到next：   cur.next = ...., cur = cur.next

一步步走，不要next.next跳。可以每次先node.next = ....然后再node = node.next.

2种reverse方法,都是循环首位相接



2种reverse方法,都是循环首位相接

只改变中间指针指向

头插法，不断把cur后面的插入prev的后面

快慢指针

都从Head起，quick到最后位时，slow在中间或者中偏后。

循环头尾相等。

快慢指针还可以用来解两链表是否相交。

1.其中一个链表头尾相接，然后判断另一个链表是否有环

2.相交链表从相遇开始有同样尾节点。2个链表一起走到尾部，看尾部是否相同。

快慢指针相遇时候，相差距离是一个环。

环的问题总结：[https://blog.csdn.net/liuxialong/article/details/6555850](https://blog.csdn.net/liuxialong/article/details/6555850)

[https://blog.csdn.net/liuxialong/article/details/6556096](https://blog.csdn.net/liuxialong/article/details/6556096)

判断2个链表相交：

1 人为构环，将链表A的尾节点指向链表B，再判断是否构环成功？从链表B的头指针往下遍历，如果能够回到B，则说明相交

2 2个栈，一直弹出来直到遇到第一个不一样的点，前面一个就是相交点

3 直接比较AB链表的尾结点是否相等即可 [https://blog.csdn.net/linchonghui888/article/details/79896127](https://blog.csdn.net/linchonghui888/article/details/79896127)

[https://leetcode-cn.com/problems/intersection-of-two-linked-lists/](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

