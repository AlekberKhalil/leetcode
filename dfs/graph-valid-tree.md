# Graph Valid Tree

Given`n`nodes labeled from`0`to`n-1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

**Example 1:**

```text
Input:
n = 5
, and 
edges = [[0,1], [0,2], [0,3], [1,4]]
Output:
 true
```

**Example 2:**

```text
Input:
n = 5, 
and 
edges = [[0,1], [1,2], [2,3], [1,3], [1,4]]
Output:
 false
```

**Note**: you can assume that no duplicate edges will appear in`edges`. Since all edges are undirected,`[0,1]`is the same as`[1,0]`and thus will not appear together in`edges`.

分析

DFS

建图 graph = {i:\[\] for i in range\(n\)}，无方向所以双向

从node 0起for loop，no cycle\(dfs\) and len\(seen\) ==n

seen这里做visited，不需要弹出因为树不回头

注意all用法。要排除grandparent!=neighbor是因为双向图，排除2个点互指的情况。

```text
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:        
        seen = set()
        graph = {i:[] for i in range(n)}
        for e in edges:#undirected
            graph[e[0]].append(e[1])
            graph[e[1]].append(e[0])
        return self.dfs(graph,seen,0,-1) and len(seen) == n


    def dfs(self, graph, seen,node,parent):
        if node in seen:
            return False
        seen.add(node)
        return all([self.dfs(graph,seen,n,node) for n in graph[node] if n!=parent]) #child!=grandparent
```

bfs

start from any node and delete every node we meet during the BFS. If there is any node left, then there is an isolated component.

注意dict pop用法，no isolated component =no cycle.

```text
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:        
        if len(edges) != n-1: return False #别忘了这个!!!!!!!!
        g,q = {i:[] for i in range(n)},[0]
        for a,b in edges:#undirected
            g[a].append(b)
            g[b].append(a)
        for i in q:
            q+=g.pop(i,[])
        return not g
```

Union find

union two nodes that are already in the same group, then there is a cycle.

```text
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:        
        if len(edges) != n-1: return False #别忘了这个
        f = list(range(n))
        def find(x):
            if f[x]!=x:
                f[x] = find(f[x])
            return f[x]   
        for a,b in edges:
            fa,fb = find(a),find(b)
            if fa==fb:
                return False
            f[fa] = fb
        return True
```

