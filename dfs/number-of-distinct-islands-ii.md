# Number of Distinct Islands II

Given a non-empty 2D array`grid`of 0's and 1's, an**island**is a group of`1`'s \(representing land\) connected 4-directionally \(horizontal or vertical.\) You may assume all four edges of the grid are surrounded by water.

Count the number of**distinct**islands. An island is considered to be the same as another if they have the same shape, or have the same shape after**rotation**\(90, 180, or 270 degrees only\) or**reflection**\(left/right direction or up/down direction\).

**Example 1:**

```text
11000100000000100011
```

Given the above grid map, return

`1`

.

Notice that:

```text
111
```

and

```text
 111
```

are considered

**same**

island shapes. Because if we make a 180 degrees clockwise rotation on the first island, then two islands will have the same shapes.

**Example 2:**

```text
11100100010100101110
```

Given the above grid map, return

`2`

.

Here are the two distinct islands:

```text
1111
```

and

```text
11
```

Notice that:

```text
1111
```

and

```text
1111
```

are considered

**same**

island shapes. Because if we flip the first array in the up/down direction, then they have the same shapes.

**Note:**The length of each dimension in the given`grid`does not exceed 50.

分析

dfs每个块标记-1，然后每个块里8个方向变形加入set pool里

```text
Scan the matrix, each time when 1 is found, search the nearby 1, push them inside a queue and mark them as -1.It is important to use the information inside the queue. As we know, the queue stands for a specific shape of an island.i. Push the island to the left upper corner by subtracting the original data with its minimum axis value.ii. Sort the queue and tuple it to avoid redundancy.iii. Find its x-axis mirror: (x,y) --> (-x,y)iv. Find its y-axis mirror: (x,y) --> (x,-y)v. Find its origin mirror: (x,y) --> (-x,-y)vi. Find its diagonal mirror: (x,y) --> (y,x)vii. Repeat 2.3, 2.4, and 2.5 on the diagonal mirror island.viii. Add all these 8 islands into the poolThere are several tricks are used here:Augment the original matrix (grid) with a row of zeros and a column of zeros. This is to avoid the check of index every single timeInstead of using another matrix to store the visited element, I directly change the value in place. -1 indicates visited. You can use a deep copy if you do not like change value in place.The element in the queue is centered by subtracting the minimum x and minimum y and then sorted, so that this shape of island will be unique.
```

```text
class Solution(object):    def numDistinctIslands2(self, grid: List[List[int]]) -> int:        if not grid or not grid[0]:            return 0        n, m = len(grid), len(grid[0])        res = 0        pool = set()        d = [-1, 0, 1, 0, -1]        grid.append([0] * m)        for row in grid: row.append(0)        def form(q):            nonlocal res, pool            mini, minj = min(x for x, y in q), min(y for x, y in q)            f1 = tuple(sorted((i - mini, j - minj) for i, j in q))            if f1 in pool: return None            res += 1            maxi, maxj = max(x for x, y in f1), max(y for x, y in f1)            f2 = tuple(sorted((maxi - i, j) for i, j in f1))            f3 = tuple(sorted((i, maxj - j) for i, j in f1))            f4 = tuple(sorted((maxi - i, maxj - j) for i, j in f1))            f5 = tuple(sorted((j, i) for i, j in f1))            f6 = tuple(sorted((maxj - i, j) for i, j in f5))            f7 = tuple(sorted((i, maxi - j) for i, j in f5))            f8 = tuple(sorted((maxj - i, maxi - j) for i, j in f5))            pool |= set([f1, f2, f3, f4, f5, f6, f7, f8])        def bfs(i, j):            q = [(i, j)]            grid[i][j] = -1            nxy = [(i + d[k+1], j + d[k]) for k in range(4)]            for i, j in q:                for nx, ny in [(i-1,j),(i+1,j),(i,j-1),(i,j+1)]:                    if grid[nx][ny] == 1:                        grid[nx][ny] = -1  # missing                        q.append((nx, ny))            form(q)        for i in range(n):            for j in range(m):                if grid[i][j] == 1:                    bfs(i, j)        return res
```

