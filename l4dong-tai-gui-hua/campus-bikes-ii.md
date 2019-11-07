# Campus Bikes II

On a campus represented as a 2D grid, there are`N`workers and`M`bikes, with`N <= M`. Each worker and bike is a 2D coordinate on this grid.

We assign one unique bike to each worker so that the sum of the Manhattan distances between each worker and their assigned bike is minimized.

The Manhattan distance between two points`p1`and`p2`is`Manhattan(p1, p2) = |p1.x - p2.x| + |p1.y - p2.y|`.

Return the minimum possible sum of Manhattan distances between each worker and their assigned bike.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/03/06/1261_example_1_v2.png)

```text
Input: workers = [[0,0],[2,1]], bikes = [[1,2],[3,3]]Output: 6Explanation: We assign bike 0 to worker 0, bike 1 to worker 1. The Manhattan distance of both assignments is 3, so the output is 6.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/03/06/1261_example_2_v2.png)

```text
Input: workers = [[0,0],[1,1],[2,0]], bikes = [[1,0],[2,2],[2,1]]Output: 4Explanation: We first assign bike 0 to worker 0, then assign bike 1 to worker 1 or worker 2, bike 2 to worker 2 or worker 1. Both assignments lead to sum of the Manhattan distances as 4.
```

**Note:**

1. `0`

   `<`

   `= workers[i][0], workers[i][1], bikes[i][0], bikes[i][1]`

   `<`

   `1000`

2. All worker and bike locations are distinct.
3. `1`

   `<`

   `= workers.length`

   `<`

   `= bikes.length`

   `<`

   `= 10`

分析

dp\[worker\]\[state\]

因为每个worker可以选N个车，所以用bit 做状态。类似 can I win

注意这里set和get用法

```text
class Solution:    def assignBikes(self, workers: List[List[int]], bikes: List[List[int]]) -> int:        def dis(x1, y1, x2, y2):            return abs(x1 - x2) + abs(y1 - y2)        B, W = len(bikes), len(workers)        dp = [[float('inf')] * ((1<<B)+1) for _ in range(W+1)]        dp[0][0] = 0        for i, worker in enumerate(workers):            for bit_bike in range((1<<B)):                for j, bike in enumerate(bikes):                    _get = bit_bike & (1<<j)                    _set = bit_bike | (1<<j)                    if not _get:                                                dp[i + 1][_set] = min( dp[i + 1][_set],                             dp[i][bit_bike] + dis(*worker, *bike))                                                 return min(dp[-1])
```

DFS

```text
class Solution:    def assignBikes(self, workers: List[List[int]], bikes: List[List[int]]) -> int:        B, W = len(bikes), len(workers)        mm = {}                def dis(x1, y1, x2, y2):            return abs(x1 - x2) + abs(y1 - y2)        def dfs(w, st):            if (w,st) in mm:                return mm[(w,st)]            if w == W:                return 0            curdis = float('inf')            for b in range(B):                if st & (1<<b) == 0:                    curdis = min(curdis, dfs(w+1, st | (1<<b)) + dis(*workers[w],*bikes[b]))            mm[(w,st)] = curdis            return curdis        return dfs(0,0)
```

