# Largest Sum of Averages

We partition a row of numbers`A` into at most`K`adjacent \(non-empty\) groups, then our score is the sum of the average of each group. What is the largest score we can achieve?

Note that our partition must use every number in A, and that scores are not necessarily integers.

```text
Example:Input:A = [9,1,2,3,9]K = 3Output: 20Explanation:The best choice is to partition A into [9], [1, 2, 3], [9]. The answer is 9 + (1 + 2 + 3) / 3 + 9 = 20.We could have also partitioned A into [9, 1], [2], [3, 9], for example.That partition would lead to a score of 5 + 2 + 6 = 13, which is worse.
```

**Note:**

* ```text
  1 <= A.length <= 100.1 <= A[i] <= 10000.1 <= K <= A.length.Answers within 10^-6 of the correct answer will be accepted as correct.
  ```

分析

最后一组长度可变，用j分割，\[j,i\]之间的avg + 前面的dp

```text
f[i][j] = max {f[p][j-1] + (A[p+1] + A[p+2] + ... + A[i]) / (i - p)}, p = 0,1,...,i-1
```

```text
class Solution:    def largestSumOfAverages(self, A: List[int], K: int) -> float:        n = len(A)        dp = [[float('-inf')] * (n+1) for _ in range(K+1)]        dp[0][0] = 0.0        for k in range(1, K+1):            for i in range(1, n+1):                   if k == 1:                    dp[k][i] = sum(A[:i])/len(A[:i]) # len(A[:i]) = i                else:                    if i < k:                        continue                    for j in range(i):                        dp[k][i] = max(dp[k][i], dp[k-1][j] + sum(A[j:i])/len(A[j:i])) # len(A[j:i]) = i=j                        #分割考虑最后一个数，dp[k-1][j]不含最后数，A[j:i]是最后一个数        return dp[K][n]
```

DFS

截两段，一段平均数+新dfs

```text
res = max(res,dfs(k-1,i) + sum(A[i:n])/(n-i))
```

K作为结束条件，k==1 和 k&gt;n. n作为for loop条件来分割。

loop n, max\(dfs前k-1组到i + 最后一组\[i,n\]的平均数\)，注意这里倒序

这里传入状态和最后尾数，下一次dfs以当前截断的尾数继续开始。

**dfs剩下新尾 + 尾部到当前index的平均数（尾组）**

另一种dfs正序的话：

**从头开始算到当前index的平均数（头组） + 剩下新头的dfs**

```text
max( averages of the current partition which starts at start + largest sum of averages which starts at tail + 1 )
```

```text
class Solution:    def largestSumOfAverages(self, A: List[int], K: int) -> float:        N = len(A)        mm = {}        def dfs(k,n):            if (k,n) in mm:                return mm[(k,n)]            if n<k:                return 0            if k == 1:                mm[(k,n)] = sum(A[:n])/n                return mm[(k,n)]            res = float('-inf')                for i in range(n-1,-1,-1):                res = max(res,dfs(k-1,i) + sum(A[i:n])/(n-i))            mm[(k,n)] = res            return res        return dfs(K,N)
```

