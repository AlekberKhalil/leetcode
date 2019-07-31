# Cheapest Flights Within K Stops

```text
There are n cities connected by m flights. Each fight starts from city u and arrives at v with a price w.

Now given all the cities and flights, together with starting city src and the destination dst, your task is to find the cheapest price from src to dst with up to k stops. If there is no such route, output -1.

Example 1:
Input: 
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 1
Output: 200
Explanation: 
The graph looks like this:


The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.
Example 2:
Input: 
n = 3, edges = [[0,1,100],[1,2,100],[0,2,500]]
src = 0, dst = 2, k = 0
Output: 500
Explanation: 
The graph looks like this:


The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.
Note:

The number of nodes n will be in range [1, 100], with nodes labeled from 0 to n - 1.
The size of flights will be in range [0, n * (n - 1) / 2].
The format of each flight will be (src, dst, price).
The price of each flight will be in the range [1, 10000].
k is in the range of [0, n - 1].
There will not be any duplicated flights or self cycles.
```

分析

dp\[k\]\[dst\] 不需要src，src用来初始化dp\[k\]\[src\]= 0，这里dp思想和ballman算法一样。只是ballman降维

注意这里K的值

```text
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:

        f = [[float('inf')]*n for _ in range(K+2)]
        f[0][src] = 0

        for k in range(1,K+2): 
            f[k][src] = 0
            for s,d,p in flights:
                f[k][d] = min(f[k][d],f[k-1][s]+p)                   

        return f[K+1][dst] if f[K+1][dst]!=float('inf') else -1
```

Ballman

这里之所以2个C ,c交换，是因为结果可能不存在：1 不存在最短路径 2 最短路径需要超过K步。如果直接在原数组上更新，无法得知最后结果是否存在，除非每次都用新的数组。K步以后如果dst没被更新，还是float\('inf'\)，结果不存在。

```text
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        C=[float('inf')]*(n)
        C[src] = 0
        for k in range(K+1):
            c=[float('inf')]*(n)
            c[src] = 0
            for s,d,p in flights:
                c[d]  = min(c[d],C[s]+p)
            C = c
        return C[dst] if C[dst] != float('inf') else -1
```

DFS

每次都是按着比当前距离小继续dfs，谁先到终点就是答案。因为限制&lt;=k，K耗尽时候也就返回。可以不必==k才返回。

```text
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        g = {}
        for s,d,p in flights:
            if s in g:
                g[s].append((d,p))
            else:
                g[s] = [(d,p)]
        seen = set()
        res = float('inf')
        def dfs(s,w,k):            
            nonlocal res            
            if s == dst :
                res = w
                return  #不到K也可以直接返回，题目要求<=k 
            if k == 0:
                return

            if s in g:                
                for ns,ws in g[s]:
                    if ns not in seen and w+ws < res:
                        seen.add(ns)
                        dfs(ns,w+ws,k-1)
                        seen.remove(ns)


        dfs(src,0,K+1)
        return -1 if res == float('inf') else res
```

BFS:PQ

```text
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        g = {}
        for s,d,p in flights:
            if s in g:
                g[s].append((d,p))
            else:
                g[s] = [(d,p)]
        seen = set()

        q = [(0,src,K+1)]
        #seen.add(src) #可能不断经过某点来更新最短距离，所以不用seen?

        while q:
            p,d,k = heapq.heappop(q)
            if d == dst:
                return p

            if d in g:
                for nd,np in g[d]:
                    if k>0:
                        #seen.add(nd)
                        heapq.heappush(q,(p+np,nd,k-1))

        return -1
```

不用pq的bfs

```text
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        g = {}
        for s,d,p in flights:
            if s in g:
                g[s].append((d,p))
            else:
                g[s] = [(d,p)]
        q = [(0,src,K+1)]

        res = float('inf')
        while q:
            p,d,k = q.pop(0)
            if d == dst:
                res = min(res,p)

            if d in g:
                for nd,np in g[d]:                    
                    if k>0 and p+np < res:  #比结果小才进入q                                           
                        q.append((p+np,nd,k-1))

        return res if res!=float('inf') else -1
```

