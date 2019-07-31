# Soup Servings

There are two types of soup: type A and type B. Initially we have`N`ml of each type of soup. There are four kinds of operations:

1. Serve 100 ml of soup A and 0 ml of soup B
2. Serve 75 ml of soup A and 25 ml of soup B
3. Serve 50 ml of soup A and 50 ml of soup B
4. Serve 25 ml of soup A and 75 ml of soup B

When we serve some soup, we give it to someone and we no longer have it. Each turn, we will choose from the four operations with equal probability 0.25. If the remaining volume of soup is not enough to complete the operation, we will serve as much as we can. We stop once we no longer have some quantity of both types of soup.

Note that we do not have the operation where all 100 ml's of soup B are used first.

Return the probability that soup A will be empty first, plus half the probability that A and B become empty at the same time.

```text
Example:
Input:
 N = 50

Output:
 0.625

Explanation:

If we choose the first two operations, A will become empty first. For the third operation, A and B will become empty at the same time. For the fourth operation, B will become empty first. So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.25 * (1 + 1 + 0.5 + 0) = 0.625.
```

**Notes:**

* `0`

  `<`

  `= N`

  `<`

  `= 10^9`

  . 

* Answers within 

  `10^-6`

   of the true value will be accepted as correct.

分析

dp bottom up，dp\[N\]\[N\] = 1倒着开始，同时dp\[0\]\[0\]按条件做。 N》4800直接返回1

为防止N太大，都%25

```text
class Solution:
    def soupServings(self, N: int) -> float:
        # Q, R = divmod(N, 25)
        # N = Q + (R > 0)
        if N > 4800: return 1
        N = math.ceil(N / 25.0) #直接用25倍数做，防止N过大。
        # if N >= 500: return 1
        dp = [[0]*(N+1) for _ in range(N+1)]
        dp[N][N] = 1
        ops = [(4,0),(3,1),(2,2),(1,3)]
        for i in range(N,0,-1):
            for j in range(N,0,-1):                
                for x,y in ops:
                    tem1=0 if i-x<=0 else i-x
                    tem2=0 if j-y<=0 else j-y
                    dp[tem1][tem2]+=dp[i][j]*0.25 #以上不包含0，0单独出来做，就是有多少serve多少
        return sum(dp[0][i] for i in range(1, N+1)) + dp[0][0]*0.5
```

DFS

注意最后N = CEIL\(N/25\)

```text
class Solution:
    def soupServings(self, N: int) -> float:

        mm = {}
        def dfs(a,b):   
            if (a,b) in mm:
                return mm[(a,b)]
            if a<=0 and b <=0: return 0.5
            if a <=0 : return 1
            if b<=0: return 0
            mm[(a,b)] = 0.25*(dfs(a-4,b)+dfs(a-3,b-1)+dfs(a-2,b-2)+dfs(a-1,b-3))
            return mm[(a,b)]
        n = math.ceil(N/25.0)
        return dfs(n,n)
```

