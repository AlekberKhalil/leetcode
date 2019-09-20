# 线段树&binary index tree

1 update更新区间和点，更新点不需要lazy. 更新区间需要lazy，有增和替换之分，而且sum需要lazy\*（r-l）。

2 pushup往上更新是必须的，左右更新完再更新root，和之前步骤一样。query也是读root的值

3 pushdown 往下推迟更新，每次更新左右孩子并且标记。在update/query里都需要，除掉pushdown 别的代码都一样

4 query 查询范围&gt; root范围可以直接返回。

线段树实例calendar ii

[https://leetcode.com/problems/my-calendar-ii/discuss/382796/Python-segment-tree](https://leetcode.com/problems/my-calendar-ii/discuss/382796/Python-segment-tree)

区间增

{% embed url="http://www.ishenping.com/ArtInfo/294138.html" %}

区间替换

[https://hrbust-acm-team.gitbooks.io/acm-book/content/data\_structure/ds\_part3.html](https://hrbust-acm-team.gitbooks.io/acm-book/content/data_structure/ds_part3.html)

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



2种：node结构也不一样。

或者是求一段index内的sum（range sum）或者count\(count of smaller, reverser pair\). 这里index是排序后的index

或者是求一段值范围内的count\(count of range sum\)

