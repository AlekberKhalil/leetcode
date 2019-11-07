# Number of Connected Components in an Undirected Graph\(UF and DFS\)

Given`n`nodes labeled from`0`to`n - 1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to find the number of connected components in an undirected graph.

**Example 1:**

```text
Input: 
n = 5
 and 
edges = [[0, 1], [1, 2], [3, 4]]


     0          3
     |          |
     1 --- 2    4 


Output: 
2
```

**Example 2:**

```text
Input: 
n = 5
 and 
edges = [[0, 1], [1, 2], [2, 3], [3, 4]]


     0           4
     |           |
     1 --- 2 --- 3


Output:  
1
```

**Note:**  
You can assume that no duplicate edges will appear in`edges`. Since all edges are undirected,`[0, 1]`is the same as`[1, 0]`and thus will not appear together in`edges`.

分析

Union find

记得find 要返回x或者f\[x\]

nested function, find可以操作father array但是union不能操作res，可能是因为primitive value?

```text
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        if not edges or not edges[0]:
            return n


        f = [i for i in range(n)]

        def find(x):
            if f[x] == x:
                return x
            f[x] = find(f[x])
            return f[x]



        for i, j in edges:
            px = find(i)
            py = find(j)
            if px != py:
                f[px] = py
                n -= 1

        return n
```

dfs

每个点开始dfs穷尽所有可达路，visited标记点，visited不需标记再去标记。

每个开端就是一个新group。

```text
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        if not edges or not edges[0]:
            return n
        visited = [0]*n
        g = {i:[] for i in range(n)}
        for x,y in edges:#无向图，2边都要加
            g[x].append(y)
            g[y].append(x)
        res = 0
        for i in range(n):
            if not visited[i]:
                self.dfs(g,i,visited,-1)
                res += 1
        return res
    def dfs(self,g,i,visited,parent):
        if visited[i]:
            return
        visited[i]=1
        for k in g[i]:
            if k!=parent:#无向图，要排除互相指向的情况
                self.dfs(g,k,visited,i)
```

BFS

```text
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        if not edges or not edges[0]:
            return n
        visited = [0]*n
        g = {i:[] for i in range(n)}
        for x,y in edges:#无向图，2边都要加
            g[x].append(y)
            g[y].append(x)
        res = 0

        for i in range(n):
            if not visited[i]:
                q = [i]
                while q:
                    cur = q.pop()
                    visited[cur] = 1
                    for k in g[cur]:
                        if not visited[k]:
                            q.append(k)
                res += 1
        return res
```

