# LRU Cache

Design and implement a data structure for[Least Recently Used \(LRU\) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations:`get`and`put`.

`get(key)`- Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`put(key, value)`- Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**  
Could you do both operations in**O\(1\)**time complexity?

**Example:**

```text
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

分析

一直错的:

get 不记得删除链表的旧位置：

**dict只有拿node的作用，只有满删**, list存在就删   

一个双链表和一个dict.自建一个LRUNode class

链表删除在原地做简单，直接原地做。链表插入尾部写成函数

 LL remove cur and insert cur

set:

```text
    # 1 dict 有：更新node值， LL remove cur and insert cur
    # 2 超过容量：去dict 里head， 去LL head 腾位置
    # 3 dict 无：建新Node, dict insert and LL insert cur(new)
```

```text
import collections


class LRUNode:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None


class LRUCache:

    # 基本元素 1dict 2双链表 3 头尾指针，还要记得互指
    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.capacity = capacity
        self.dict = collections.defaultdict(LRUNode)
        self.head = LRUNode(0, 0)
        self.tail = LRUNode(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    # LL removecur and insert cur
    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        # update LL: remove cur and insert cur
        if key not in self.dict:
            return -1
        node = self.dict[key]
        # remove cur
        node.prev.next = node.next
        node.next.prev = node.prev
        # insert cur
        self.insertLL(node)

        return node.value

    # 1 dict 有：更新node值， LL remove cur and insert cur
    # 2 超过容量：去dict 里head， 去LL head 腾位置
    # 3 dict 无：建新Node, dict insert and LL insert cur(new)
    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: void
        """
        if key in self.dict:
            self.dict[key].value = value  # update node's value
            self.get(key)  # update LL cur
            return

        # make space for new node first
        #唯一一处删dict
        if len(self.dict) == self.capacity:
            node = self.head.next
            del self.dict[node.key]
            self.head.next = node.next
            node.next.prev = self.head

        newNode = LRUNode(key, value)
        self.dict[key] = newNode
        self.insertLL(newNode)

    # LL insert node
    def insertLL(self, node):
        # prevs then nexts
        node.prev = self.tail.prev
        self.tail.prev = node
        node.prev.next = node
        node.next = self.tail

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

