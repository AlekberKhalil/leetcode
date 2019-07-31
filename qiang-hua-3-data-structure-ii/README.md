# 强化3（data structure II\)

## Heap

### 矩阵小技巧从外向内，然后标记visit\(Trapping Rain Water II\)

* 用数组表示，满二叉树 , 从0开始的话父 \(id-1\)/2  子id\*2+1 id\*2+2
* 插入push 直接加入数组末端 siftup o\(log n\)
* 删除pop 堆顶和末尾元素交换，然后直接删除末尾。siftdown  o\(log n\)
* remove 先find o\(n\) 和末尾元素交换。删除末尾以后，交换的元素可siftup/down

## hashheap

* 和heap区别：heap底部用数组，hashheap底部是hash，上面都是堆（树）
* delete时间复杂度不一样，对于find，可以利用hash快速找，hash加速堆查询o\(log n\)
* java里就是priority queue

LRU: linked hash 下面hash,上面double linked list

