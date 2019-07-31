# Most Stones Removed with Same Row or Column

On a 2D plane, we place stones at some integer coordinate points. Each coordinate point may have at most one stone.

Now, a\_move\_consists of removing a stone that shares a column or row with another stone on the grid.

What is the largest possible number of moves we can make?

**Example 1:**

```text
Input: 
stones = 
[[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 
5
```

**Example 2:**

```text
Input: 
stones = 
[[0,0],[0,2],[1,1],[2,0],[2,2]]
Output: 
3
```

**Example 3:**

```text
Input: 
stones = 
[[0,0]]
Output: 
0
```

**Note:**

```text
1 <= stones.length <= 1000
0 <= stones[i][j] < 10000
```

分析

每个石头把行列连起来变成一个岛，答案就是移到每个岛只剩一个石头。

这里DFS就是loop每个点，把行列连起来。 优化是把行列范围打散，行在1-N,j+10000列在N-2N，区分行列。

简单把i,j当做数字相连就好，就能理解打散区间的做法

参考[https://www.jianshu.com/p/30d2058db7f7](https://www.jianshu.com/p/30d2058db7f7)

DFS

```text
class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:
        index = collections.defaultdict(set)
        for i, j in stones:
            index[i].add(j+10000)
            index[j+10000].add(i)
        seen = set()
        islands = 0
        def dfs(i):            

            seen.add(i)
            for j in index[i]:
                if j not in seen:
                    dfs(j)
        for i,j in stones:
            if i not in seen:
                dfs(i) #i里的cols 全部相连
                dfs(j+10000)#i里的rows 全部相连
                islands += 1
        return len(stones) - islands
```

Union Find

UNION FIND （i，~j\)也是，等于把j映射到j+10000。~j是补码，就是二进制code倒过来。

```text
class Solution:
    def removeStones(self, stones: List[List[int]]) -> int:
        f  = {}

        def find(x):
            if f[x]!=x:
                f[x] = find(f[x])
            return f[x]
        def union(x,y):
            f.setdefault(x,x)
            f.setdefault(y,y)
            f[find(x)] = find(y)
        for x,y in stones:
            union(x,~y)
        return len(stones) - len({find(x) for x in f})#点数-岛数
```

