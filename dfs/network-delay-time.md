# Network Delay Time

There are`N`network nodes, labelled`1`to`N`.

Given`times`, a list of travel times as**directed**edges`times[i] = (u, v, w)`, where`u`is the source node,`v`is the target node, and`w`is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node`K`. How long will it take for all nodes to receive the signal? If it is impossible, return`-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png)

```text
Input: times = [[2,1,1],[2,3,1],[3,4,1]], N = 4, K = 2
Output: 2
```

**Note:**

```text
N will be in the range [1, 100].
K will be in the range [1, N].
The length of times will be in the range [1, 6000].
All edges times[i] = (u, v, w) will have 1 <= u, v <= N and 0 <= w <= 100.
```

分析

DFS：从起始到每个点，记录到该点最小距离。最大的那个距离就是答案，如果有点未遍历则-1

比较带记忆的dfs是dict+dfs返回，此处是dict+dfs带参数

```text
class Solution:
    def networkDelayTime(self, times: List[List[int]], N: int, K: int) -> int:
        g = collections.defaultdict(list)
        for s,d,t in times:
            g[s].append((t,d))

        dist = {node:float('inf') for node in range(1,N+1)}

        #带记忆的dfs是dict+dfs返回，此处是dict+dfs带参数
        def dfs(s,delay):
            if delay >= dist[s]:
                return
            dist[s] = delay
            for t,d in sorted(g[s]):
                dfs(d,delay+t)


        dfs(K,0) 
        ans = max(dist.values())
        return -1 if ans==float('inf') else ans
```

用dfs返回带记忆的做法，只能得到每个点最短距离，但是本题需要得到每个点最短距离之后，从起点开始最长的点。

```text
class Solution:#用dfs返回带记忆的做法 错的，此处做比较
   def networkDelayTime(self, times: List[List[int]], N: int, K: int) -> int:
        g = {}
        for s, d, t in times:
            if s not in g:
                g[s] = [(t, d)]
            else:
                g[s].append((t, d))

        dist = {}

        def dfs(s):
            if s in dist:
                return dist[s]

            if s not in g:
                return 0
            res = float('inf')
            for t, d in sorted(g[s]):
                res = min(res, t + dfs(d))
            dist[s]=res
            return dist[s]

        ans = dfs(K)
        return ans
```

BFS

## Dijkstra's Algorithm <a id="approach-2-dijkstras-algorithm-accepted"></a>

heap:

```text
class Solution:
    def networkDelayTime(self, times: List[List[int]], N: int, K: int) -> int:
        g = collections.defaultdict(list)
        for s,d,t in times:
            g[s].append((t,d))

        dist = {}

        q = [(0,K)]
        #dist[K] = 0
        while q:
            d,n = heapq.heappop(q)
            if n in dist:
                continue
            dist[n] = d
            for w,v in g[n]:
                if v not in dist:
                    heapq.heappush(q,(w+d,v)) 


        return max(dist.values()) if len(dist) ==N else -1
```

