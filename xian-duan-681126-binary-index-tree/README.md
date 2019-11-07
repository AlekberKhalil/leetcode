# 线段树&binary index tree

做这类题目

1 分治 mid = （L+R）/2，左右recursive后，merge,不要忘了LR内要sort

2 BST ：insert and sort，每个Node内存比它greater/equal的count

3 binary index tree ：，在sorted 数组里，update是更新比它大的数。get是取比它小的数sum。

count of smaller numbers: 取比它小的数，所以update query常规。

reverse pairs：取大于2\*当前数的数，所以update query反向。

这两题都是需要根据前数顺序得到当前，所以要动态Update。而且**都是用sorted 的Index来建树。**

range sum静态update

4 segment tree

5 只要取比当前数大/小的数的个数，直接Index建树就好，然后Update加权重。 除非像count of range sum、range sum一样 需要val的范围，才需要用到数的值建树。

