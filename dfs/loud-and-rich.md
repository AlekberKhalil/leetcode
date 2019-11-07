# Loud and Rich

In a group of N people \(labelled`0, 1, 2, ..., N-1`\), each person has different amounts of money, and different levels of quietness.

For convenience, we'll call the person with label`x`, simply "person`x`".

We'll say that`richer[i] = [x, y]`if person`x` definitely has more money than person `y`. Note that`richer` may only be a subset of valid observations.

Also, we'll say`quiet[x] = q`if personx has quietness`q`.

Now, return`answer`, where`answer[x] = y`if`y`is the least quiet person \(that is, the person`y`with the smallest value of`quiet[y]`\), among all people who definitely have equal to or more money than person`x`.

**Example 1:**

```text
Input: 
richer = 
[[1,0],[2,1],[3,1],[3,7],[4,3],[5,3],[6,3]]
, quiet = 
[3,2,5,4,6,1,7,0]
Output: 
[5,5,2,5,4,5,6,7]
Explanation: 

answer[0] = 5.
Person 5 has more money than 3, which has more money than 1, which has more money than 0.
The only person who is quieter (has lower quiet[x]) is person 7, but
it isn't clear if they have more money than person 0.

answer[7] = 7.
Among all people that definitely have equal to or more money than person 7
(which could be persons 3, 4, 5, 6, or 7), the person who is the quietest (has lower quiet[x])
is person 7.

The other answers can be filled out with similar reasoning.
```

**Note:**

```text
1 <= quiet.length = N <= 500
0 <= quiet[i] < N, all quiet[i] are different.
0 <= richer.length <= N * (N-1) / 2
0 <= richer[i][j] < N
richer[i][0] != richer[i][1]
richer[i]'s are all different.
The observations in richer are all logically consistent.
```

分析

DFS建图，比自己大的放list。dfs list里选quiet最小的。也是带memo的

简缩版

```text
class Solution:
    def loudAndRich(self, richer: List[List[int]], quiet: List[int]) -> List[int]:
        g = collections.defaultdict(list)
        for u,v in richer:
            g[v].append(u)
        n = len(quiet)
        res = [-1]*n

        def dfs(i):
            if res[i] < 0:            
                res[i] = min([dfs(j) for j in g[i]] + [i], key = lambda x: quiet[x]) #不要忘了Key，也不要忘了加[i]自己。
            return res[i]
        return list(map(dfs, range(n))) #dfs没有()
```

扩展板DFS

```text
class Solution:
    def loudAndRich(self, richer: List[List[int]], quiet: List[int]) -> List[int]:
        g = collections.defaultdict(list)
        for u,v in richer:
            g[v].append(u)
        n = len(quiet)
        res = [-1]*n

        def dfs(i):
            if res[i] >= 0: 
                return res[i]
            res[i] = i
            for j in g[i]:
                if quiet[res[i]] > quiet[dfs(j)]:
                    res[i] = res[j]
            return res[i]
        return list(map(dfs, range(n))) #dfs没有()
```

BFS

富点跟一串穷点。富点入度0，topo排序

res\[\]里指向的是比他富切比他安静的人

```text
class Solution:
    def loudAndRich(self, richer: List[List[int]], quiet: List[int]) -> List[int]:
        g = collections.defaultdict(list)
        indegree = collections.defaultdict(int)
        for u,v in richer:
            g[u].append(v)
            indegree[v] += 1
        n = len(quiet)
        res = [i for i in range(n)] #初始赋值为点本身
        q = [i for i in range(n) if indegree[i] == 0]
        while q:
            cur = q.pop()
            for nxt in g[cur]:
                if quiet[res[nxt]] > quiet[res[cur]]:#quiet[res[nxt]]  不是直接quiet[nxt] 
                         res[nxt] = res[cur]
                indegree[nxt] -= 1
                if indegree[nxt] == 0:
                    q.append(nxt)
        return res
```

