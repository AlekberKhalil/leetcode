# DFS

多线程dfs BFS:

* This is really only useful if the processing of each node is expensive.  If the searching itself is what is taking most of the time then parallelization will most likely slow you down with its overhead, not speed anything up.
* For a breath first search, an unordered search, and possibly certain others, you can do the searching itself in parallel, and not just the consuming of each node, but for a depth first search that is not possible.  There is only ever one node to do next, unlike a breath first search where there are 2^\(current depth\) nodes to process at the same time

要给出所有方案的话。一般DFS

跳着走的无需visited？

比较subset和combination sum，前俩是有pos，跳着走，所以不需要visited，注意path还是需要弹入弹出，和visited不是一个东西。 

Permutation是一步步走， for 循环了每步所有可能性，必须要visited去重。

电话本也是一步步走，每个for loop循环每步所有可能性，不需要visited。

**dfs的状态**

* 每个元素有取或者不取，就2个路径。子dfs就调用2次
* 很多情况需要选择，for loop。子dfs要调用多次。
* pos是给当前位置选元素，for loop所有candidate

**combination sum**

* 前三个都是要求Unique combination
* For loop 从当前pos开始还是从0开始决定了combination是否unique。unique所以dfs参数有start，每次从start开始，for loop到结束。以此来使combination unique，不返回使用前面已经使用过的数导致乱序。比如【1，2】【2，1】就是重复的不unique。
* 每次调用子dfs时候start\(pos\)参数是否i++取决于单个元素是可以无限取还是只能取一次。I 是单个元素可重复取，所以for loop里调用的dfs i都不增加，但是II里单个元素只能取一次，所以dfs 里 i++。换句话说每次子dfs里的start\(pos）不动就是可重复，pos++了就是不可重复
* 处理Input的数组。如果每个元素可以无限取，则input要去重+排序，如果元素只能取一次，则input只需要排序
* 最后一个是所有combination的方案数，背包问题

**数组结合问题（都取，考虑结合的组合）**

如果是数组需要中间元素任意结合，中间元素结合的start,end 不能定，就用start作为dfs参数传入（pos\)。end则用for loop的i来决定

1 Expression Add Operators, for loop end 到结束

2 restore IP Addresses问题，for loop end 到3

3 palindrome

word search II : 初始就判断valid,因为叶节点也没必要继续扩展下去。同时剪枝是在for loop外，为了一个元素的时候也能判断。

**取不取问题**

1 remove invalid parenthesis 当前可取可不取，还有3个情况判断。

python:

dfs: 两种方法弹入弹出path

```text
path.append(nums[i])
self.dfs(nums,i+1,path,ret)
path.pop()

最后ret要copy path:     ret.append(list(path)) 或者 ret.append(path[:)
```

或者

```text
self.dfs(nums,i+1,path+[nums[i]],ret)

最后直接 ret.append(path)
```

combination的去重，结合Increasing Subsequences的去重。就是当前层（forloop\)一条dfs路径不能同样的数字走两遍下去，会导致重复。

combination有重复数字去重，sort+比较前后数，相等就continue

increasing sub只能用set存**当前层**是否用了本数，因为不能排序，需要保持顺序。

二维数组连通问题

Max Area of Island DFS,BFS,UNION FIND



