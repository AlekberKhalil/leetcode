# Rehashing

The size of the hash table is not determinate at the very beginning. If the total size of keys is too large \(e.g. size &gt;= capacity / 10\), we should double the size of the hash table and rehash every keys. Say you have a hash table looks like below:

`size=3`,`capacity=4`

```text
[null, 21, 14, null]
       ↓    ↓
       9   null
       ↓
      null
```

The hash function is:

```text
int hashcode(int key, int capacity) {
    return key % capacity;
}
```

here we have three numbers, 9, 14 and 21, where 21 and 9 share the same position as they all have the same hashcode 1 \(21 % 4 = 9 % 4 = 1\). We store them in the hash table by linked list.

rehashing this hash table, double the capacity, you will get:

`size=3`,`capacity=8`

```text
index:   0    1    2    3     4    5    6   7
hash : [null, 9, null, null, null, 21, 14, null]
```

Given the original hash table, return the new hash table after rehashing .

## Notice

For negative integer in hash table, the position can be calculated as follow:

* **C++/Java**

  : if you directly calculate -4 % 3 you will get -1. You can use function: a % b = \(a % b + b\) % b to make it is a non negative integer.

* **Python**

  : you can directly use -1 % 3, you will get 2 automatically.

分析

旧表每条链表traverse，都hashcode一个新index进入新表（包括header！），如果新表位置已有node，就走到该node最后插入。

记得Node是链表，所以每次要new新的，不能直接连上旧的

```text
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        // write your code here
        int n = hashTable.length;
        if(n == 0)
            return hashTable;
        int len = 2 * n;
        ListNode[] nTable = new ListNode[len];
        for(ListNode cur : hashTable){
            while(cur != null){
                int nIndex = hashcode(cur.val, len);
                if(nTable[nIndex] == null){
                    nTable[nIndex] = new ListNode(cur.val);
                }else{
                    ListNode head = nTable[nIndex];
                    while(head.next != null){
                        head = head.next;
                    }
                    head.next = new ListNode(cur.val);
                }
                cur = cur.next;
            }
        }
        return nTable;
    }

    int hashcode(int key, int capacity) {
        return (key % capacity + capacity) % capacity;
    }
};
```

