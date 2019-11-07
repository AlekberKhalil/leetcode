# Guess Number Higher or Lower II

We are playing the Guess Game. The game is as follows:

I pick a number from**1**to**n**. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

However, when you guess a particular number x, and you guess wrong, you pay**$x**. You win the game when you guess the number I picked.

**Example:**

```text
n = 10, I pick 8.First round:  You guess 5, I tell you that it's higher. You pay $5.Second round: You guess 7, I tell you that it's higher. You pay $7.Third round:  You guess 9, I tell you that it's lower. You pay $9.Game over. 8 is the number I picked.You end up paying $5 + $7 + $9 = $21.
```

Given a particular**n ≥ 1**, find out how much money you need to have to guarantee a**win**.

分析

i,j段区间用K分割，\[i,k\]和\[k,j\]取最大的（最糟情况）。然后整体\[i.j\]段取个min cost。相当于运气最差\(好保证有足够钱），但是策略最好。

```text
class Solution:    def getMoneyAmount(self, n: int) -> int:        p = [[0]*(n+1) for _ in range(n+1)]        for i in range(2,n+1):                        for j in range(i-1,0,-1):                globalMin = float('inf')                for k in range(j+1,i):#分割时i，j都不含                    globalMin = min(globalMin,k+max(p[j][k-1],p[k+1][i]))                p[j][i] = j if j+1 == i else globalMin #？？？？        return p[1][n]
```

memorize search 分治

```text
class Solution:    def getMoneyAmount(self, n: int) -> int:        p = [[0]*(n+1) for _ in range(n+1)]        def helper(s,e):            if s >= e:                return 0            if p[s][e]!=0:                return p[s][e]            globalMin = float('inf')            for k in range(s,e+1):#分割时含s,e                left = helper(s,k-1)                right = helper(k+1,e)                globalMin = min(globalMin,k+max(left,right))            p[s][e] = globalMin            return globalMin        return helper(1,n)
```

