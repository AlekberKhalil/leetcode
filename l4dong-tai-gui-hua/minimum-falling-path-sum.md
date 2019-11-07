# Minimum Falling Path Sum

Given a**square**array of integers`A`, we want the**minimum**sum of a\_falling path\_through`A`.

A falling path starts at any element in the first row, and chooses one element from each row. The next row's choice must be in a column that is different from the previous row's column by at most one.

**Example 1:**

```text
Input: [[1,2,3],[4,5,6],[7,8,9]]Output: 12Explanation: The possible falling paths are:
```

* `[1,4,7], [1,4,8], [1,5,7], [1,5,8], [1,5,9]`
* `[2,4,7], [2,4,8], [2,5,7], [2,5,8], [2,5,9], [2,6,8], [2,6,9]`
* `[3,5,7], [3,5,8], [3,5,9], [3,6,8], [3,6,9]`

The falling path with the smallest sum is`[1,4,7]`, so the answer is`12`.

**Note:**

```text
1 <= A.length == A[0].length <= 100-100 <= A[i][j] <= 100
```

分析

本 row是从前row的3个col的min来

```text
A[i][j] is the minimum of A[i - 1][j - 1], A[i - 1][j] and A[i - 1][j + 1].
```

```text
class Solution:    def minFallingPathSum(self, A: List[List[int]]) -> int:        if not A or not A[0]:            return 0        n,m = len(A),len(A[0])        dp = A[0]        for i in range(1,n):            cur = [float('inf')] *(m)            for j in range(m):                cur[j] = min(dp[max(0,j-1)],dp[j],dp[min(m-1,j+1)]) + A[i][j]            dp = cur[:]        return min(dp)
```

