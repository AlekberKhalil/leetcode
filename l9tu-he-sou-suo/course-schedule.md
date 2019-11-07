# Course Schedule

There are a total ofncourses you have to take, labeled from`0`to`n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair:`[0,1]`

Given the total number of courses and a list of prerequisite**pairs**, is it possible for you to finish all courses?

**Example 1:**

```text
Input: 2, [[1,0]] Output: trueExplanation: There are a total of 2 courses to take.              To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```text
Input: 2, [[1,0],[0,1]]Output: falseExplanation: There are a total of 2 courses to take.              To take course 1 you should have finished course 0, and to take course 0 you should             also have finished course 1. So it is impossible.
```

分析

这里图就是邻接链表

1 三个元素，图\(arraylist的数组），入度\(int\[\]或者map\)，q\(queue或者arraylist，这里可能linkedlist可以所以arraylist也可以）

2 先初始化图，就是遍历所有元素都建立一个对应链表。

3 用prerequisites来填充图和入度

4 **入度为0的放入q里，将来遍历也是入度为0就进入bfs，这里就避免的入栈再出栈**

5 遍历q，把每个元素对应的链表再遍历（--e的入度 == 0? q.add\(e\) \)

courseII 差不多。就是返回bfs,记得一定要判断bfs == n！！！！！！！

```text
    public boolean canFinish(int n, int[][] prerequisites) {        ArrayList<Integer>[] G = new ArrayList[n];        int[] degree = new int[n];        ArrayList<Integer> bfs = new ArrayList();        for (int i = 0; i < n; ++i) G[i] = new ArrayList<Integer>();        for (int[] e : prerequisites) {            G[e[1]].add(e[0]);//此处方向不要反了            degree[e[0]]++;        }        //这里入度需要遍历所有元素，loop到N        for (int i = 0; i < n; ++i) if (degree[i] == 0) bfs.add(i);        for (int i = 0; i < bfs.size(); ++i)            for (int j: G[bfs.get(i)])                if (--degree[j] == 0) bfs.add(j);        return bfs.size() == n;    }
```

