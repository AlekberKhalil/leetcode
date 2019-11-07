# Find Eventual Safe States

n a directed graph, we start at some node and every turn, walk along a directed edge of the graph. If we reach a node that is terminal \(that is, it has no outgoing directed edges\), we stop.

Now, say our starting node is\_eventually safe \_if and only if we must eventually walk to a terminal node. More specifically, there exists a natural number`K`so that for any choice of where to walk, we must have stopped at a terminal node in less than`K`steps.

Which nodes are eventually safe? Return them as an array in sorted order.

The directed graph has`N`nodes with labels`0, 1, ..., N-1`, where`N`is the length of`graph`. The graph is given in the following form:`graph[i]`is a list of labels`j`such that`(i, j)`is a directed edge of the graph.

```text
Example:Input: graph = [[1,2],[2,3],[5],[0],[5],[],[]]Output: [2,4,5,6]Here is a diagram of the above graph.
```

![Illustration of graph](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/03/17/picture1.png)

**Note:**

* `graph`

  will have length at most

  `10000`

  .

* The number of edges in the graph will not exceed

  `32000`

  .

* Each

  `graph[i]`

  will be a sorted list of different integers, chosen within the range

  `[0, graph.length - 1]`

分析

把所有入度为0的一个个移除就是答案，这里把图反向一下做dict

```text
class Solution:    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:        n = len(graph)        rg = collections.defaultdict(list)        for i in range(n):            for j in graph[i]:                rg[j].append(i)        out = [len(graph[i]) for i in range(n)]        q = [i for i in range(n) if out[i] == 0]        res = []        while q:            cur = q.pop()            res.append(cur)            for x in rg[cur]:                out[x] -= 1                if out[x] == 0:                    q.append(x)        return sorted(res)
```

DFS

```text
The idea is to just use plain DFS with a state = {Initial=0, InProgress=1, Completed=2 }.When traversing through the graph, if we detect a cycle by encountering a node which is InProgressif visited[node] == 1ORby visiting a node that is already part of a cyclenode in cycle
```

```text
class Solution:    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:        n = len(graph)        v = [0]*n        def dfs(i):            if not v[i]:                v[i] = 2            v[i] = 1                                      for j in graph[i]:                if v[j] == 1 or v[j] == 0 and not dfs(j):                    return False            v[i] = 2            return True        return list(filter(dfs,range(n))) #注意filter用法
```

