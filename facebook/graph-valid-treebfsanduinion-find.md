# Graph Valid Tree\(bfs&uinion find\)

## Graph Valid Tree

Given`n`nodes labeled from`0`to`n - 1`and a list of`undirected`edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

## Example

Given`n = 5`and`edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return true.

Given`n = 5`and`edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return false.

## Notice

You can assume that no duplicate edges will appear in edges. Since all edges are`undirected`,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in edges.

分析

图的话最后判断是否所有点都可达 len\(set\)==n

```text
class Solution:    """    @param n: An integer    @param edges: a list of undirected edges    @return: true if it's a valid tree, or false    """    def validTree(self, n, edges):        # write your code here        if len(edges) != n-1:            return False        graph = {i:[] for i in range(n)}        # indegree = {i:0 for i in range(n)}        for e in edges:            graph[e[0]].append(e[1])            graph[e[1]].append(e[0])            # indegree[e[1]] += 1        q = [0]        ss = {0}        while q:            cur = q.pop(0)            for nn in graph[cur]:                if nn not in ss:                    ss.add(nn)                    q.append(nn)        return len(ss) == n
```

并查集的话已加入的都变成一团，再加入的旧点就该返回错误（连旧点算有环）

可以看最后size是不是1或者每个edge的两端是否是共同祖先（已出现过

```text
class Solution:    """    @param n: An integer    @param edges: a list of undirected edges    @return: true if it's a valid tree, or false    """    def validTree(self, n, edges):        if len(edges) != n - 1:            return False        self.parent = {i: i for i in range(n)}        self.size = n        for a,b in edges:            # if self.find(e[0]) == self.find(e[1]):            #     return False            self.uinion(a,b)        return self.size ==1    def find(self, x):        if x == self.parent[x]:            return x        self.parent[x] = self.find(self.parent.get(x))        return self.parent[x]    def uinion(self, x, y):        rx = self.find(x)        ry = self.find(y)        if rx != ry:            self.parent[rx] = ry            self.size -= 1
```

