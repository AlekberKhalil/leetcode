# 强化2（Union Find, Trie, sweep line\)

## Union Find

1. 解决集合查询合并的数据结构，支持O（1） find O\(1\) union
2. 用hashmap
3. father 可以指向自己或者0
4. 并查集1不能拆开，2是放射状结构的数，子都指向父亲
5. time complexity : worst o\(n\) 一条直线时候，best o\(logn\) by rank: [https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)

代码模板

```text
public class UnionFind{    private int[] father = null;    //放射状，路径压缩    public int find(int x){             if(father[x] == 0)                      return x;             return father [x] = find(father[x]);//全部直接指向father，压缩路径，从列状到放射状 O（1）         }//union合并key father之间合并，和子没关系    public void union(int a, int b){             int root_a = find(a);             int root_b = find(b);             if(root_a != root_b){                      father(root_a) = root_b;             }    }}
```

Connecting Graph 问题总结

并查集原生操作

* 查询两个元素是否在同一个集合内
* 合并两个元素所在的集合

并查集派生操作

* 查询某个元素所在集合的元素个数
* 查询当前集合的个数

图的问题很可能是并查集

并查集可以用来判断数是否有环，如果2个端点已经在一个集合，则有环

## Trie 字典树

from retrieve

一个字符对应一个node，查Node的孩子，char的index插入孩子相应的pos

1.字典放入哈希表查询 2.字典建成Trie树（单词插入trie树）

Hash vs Trie

* 时间复杂度 o\(1\) o\(1\) 都对于一个字符串
* 空间复杂度Trie更好

通常用Hash 因为有库函数实现，trie要自己实现

Trie考点

* 一个一个字符串/字母遍历 
* 需要节约空间
* 查找前缀

_**代码：**_

```text
这是对单个word来说！！！！！！！Trie的insert和find都是3层代码，for里面也是3层。1 先定点初始this或者新建起点，cur = this;2 for loop里就是找pos往下走，从父到子的过程。find 和insert区别就是for loop里子空，一个新建一个返回.3 最后返回结果不同。
```

## sweep-line 扫描线

扫描问题思路

1. 事件以区间的形式存在
2. 区间两端代表事件开始和结束。拆成两个。
3. 需要**排序**

## 总结

数据结构题目

Union Find: 集合合并，查找元素在集合里面

Trie：一个字母一个字母查找，快速判断前缀

Sweep-line: 区间拆分

## Other tips

java 栈空间 32M

```text
(x,y)->id    id = mx+y -> x = id/m     y = id%m (M是矩阵宽）
```

