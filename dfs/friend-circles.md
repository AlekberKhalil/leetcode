# Friend Circles

There are**N**students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a**direct**friend of B, and B is a**direct**friend of C, then A is an**indirect**friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a**N\*N**matrix**M**representing the friend relationship between students in the class. If M\[i\]\[j\] = 1, then the ithand jthstudents are**direct**friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

**Example 1:**

```text
Input:[[1,1,0], [1,1,0], [0,0,1]]Output: 2Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. The 2nd student himself is in a friend circle. So return 2.
```

**Example 2:**

```text
Input:[[1,1,0], [1,1,1], [0,1,1]]Output: 1Explanation:The 0th and 1st students are direct friends, the 1st and 2nd students are direct friends, so the 0th and 2nd students are indirect friends. All of them are in the same friend circle, so return 1.
```

**Note:**

1. N is in range \[1,200\].
2. M\[i\]\[i\] = 1 for all students.
3. If M\[i\]\[j\] = 1, then M\[j\]\[i\] = 1.

Union Find

union里面f\[x\]=y不要再反顺序了。

```text
class Solution:    def findCircleNum(self, M: List[List[int]]) -> int:        if not M or not M[0]:            return 0        n,m = len(M),len(M[0])        f = [i for i in range(n)]        cnt = n        def find(x):            if x == f[x]:                return x            f[x] = find(f[x])            return f[x]        def union(x,y):            nonlocal cnt            fx = find(x)            fy = find(y)            if fx!=fy:                f[fx] = fy#每次都错 赋值f[x]在前                cnt -=1        for i in range(n):            for j in range(m):#可以i+1->m 都行                if M[i][j] == 1:                    union(i,j)        return cnt
```

DFS

不能看成Matrix4个方向连通问题，而是每个人单独dfs

需要visited set记录每个人是否遍历过

```text
class Solution:    def findCircleNum(self, M: List[List[int]]) -> int:        if not M or not M[0]:            return 0        n,m = len(M),len(M[0])        visited = set()        def dfs(x):            if x in visited:                return            visited.add(x)            for y in range(n):                if y not in visited and M[x][y] == 1:                    dfs(y)        res = 0               for i in range(n):            if i not in visited:                    dfs(i)                    res += 1                            return res
```

BFS

```text
class Solution:    def findCircleNum(self, M: List[List[int]]) -> int:        if not M or not M[0]:            return 0        n = len(M)        visited = set()              res = 0         def bfs(x):            q = [x]            while q:                cur = q.pop(0)                visited.add(cur)                for i in range(n):                    if i not in visited and M[cur][i] == 1:                        q.append(i)        for i in range(n):            if i not in visited:                bfs(i)                res += 1        return res
```

