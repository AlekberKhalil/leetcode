# Possible Bipartition

Given a set of`N` people \(numbered`1, 2, ..., N`\), we would like to split everyone into two groups of**any**size.

Each person may dislike some other people, and they should not go into the same group.

Formally, if`dislikes[i] = [a, b]`, it means it is not allowed to put the people numbered`a`and`b`into the same group.

Return`true` if and only if it is possible to split everyone into two groups in this way.

1. **Example 1:**

```text
Input: 
N = 
4
, dislikes = 
[[1,2],[1,3],[2,4]]
Output: 
true
Explanation
: group1 [1,4], group2 [2,3]
```

**Example 2:**

```text
Input: 
N = 
3
, dislikes = 
[[1,2],[1,3],[2,3]]
Output: 
false
```

**Example 3:**

```text
Input: 
N = 
5
, dislikes = 
[[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: 
false
```

**Note:**

```text
1 <= N <= 2000
0 <= dislikes.length <= 10000
1 <= dislikes[i][j] <= N
dislikes[i][0] < dislikes[i][1]
There does not exist i != j for which dislikes[i] == dislikes[j].
```

分析

和以往visit直接返回不同，这里visit的话就判断对错返回，否则继续bfs或者dfs

color既记录颜色（0，1），也当做seen用。每次dfs比较颜色，不对就返错。记得main里要loop 防止没有遍历过的人。

```text
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        mm = collections.defaultdict(list)
        for a,b in dislikes:
            mm[a].append(b)
            mm[b].append(a)

        color = {}
        def dfs(i,g):
            if i in color:
                return True if color[i] == g else False            
            color[i] = g
            for j in mm[i]:                
                if not dfs(j,1-g): return False
            return True

        for i in range(N):
            if i not in color and not dfs(i,0):
                    return False
        return True
```

bfs:

```text
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        mm = collections.defaultdict(list)
        for a,b in dislikes:
            mm[a].append(b)
            mm[b].append(a)

        color = {}
        def bfs(i):
            q = [i] 
            color[i] = 0
            while q:
                cur=q.pop(0)

                for j in mm[cur]:
                    if j in color:
                        if color[cur] == color[j]:
                            return False
                    else:
                        q.append(j)
                        color[j] = 1-color[cur]
            return True
        for i in range(N):
            if i not in color and not bfs(i):
                return False
        return True
```

union find

每次u和neighbor v 比较，一个爹就错，然后把所有Neighbor都Union。

```text
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        mm = collections.defaultdict(list)
        for a,b in dislikes:
            mm[a].append(b)
            mm[b].append(a)
        f = [i for i in range(1,N+1)]
        def find(x):
            if f[x-1] == x:
                return x
            f[x-1] = find(f[x-1])
            return f[x-1]

        for i in range(1,N+1):
            if i in mm:
                p1 = find(i)
                p2 = find(mm[i][0])
                if p1 == p2:
                    return False
                for j in mm[i][1:]:
                    p3 = find(j)
                    if p1 == p3:
                        return False
                    f[p3-1] = p2




        return True
```

