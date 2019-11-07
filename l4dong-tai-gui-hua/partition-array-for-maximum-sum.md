# Partition Array for Maximum Sum

Given an integer array`A`, you partition the array into \(contiguous\) subarrays of length at most`K`. After partitioning, each subarray has their values changed to become the maximum value of that subarray.

Return the largest sum of the given array after partitioning.

**Example 1:**

```text
Input: 
A = 
[1,15,7,9,2,5,10]
, K = 
3
Output: 
84

Explanation
: A becomes [15,15,15,9,10,10,10]
```

```text
Note:

1 <= K <= A.length <= 500
0 <= A[i] <= 10^6
```

分析

和上面书架题一模一样，记住这里求本段的max不能合在一起做，可能是Python计算顺序问题

```text
class Solution:
    def maxSumAfterPartitioning(self, A: List[int], K: int) -> int:
        n = len(A)
        dp = [0]*(n+1)
        for i in range(1,n+1):
            dp[i] = dp[i-1] + A[i-1]
            j = i-1
            mx = A[i-1]
            while j >0 and i - j < K: 
                mx = max(mx,A[j-1])
                dp[i] = max(dp[i],dp[j-1] + mx*(i-j+1)) #mx不能合在这里算，不知道为什么
                j-=1
        return dp[-1]
```

