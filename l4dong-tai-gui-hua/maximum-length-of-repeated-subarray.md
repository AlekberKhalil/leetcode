# Maximum Length of Repeated Subarray

Given two integer arrays`A`and`B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**

```text
Input:A: [1,2,3,2,1]B: [3,2,1,4,7]Output: 3Explanation:The repeated subarray with maximum length is [3, 2, 1].
```

**Note:**

1. 1 

   &lt;

   = len\(A\), len\(B\) 

   &lt;

   = 1000

2. 0 

   &lt;

   = A\[i\], B\[i\] 

   &lt;

    100

分析

初始化为0，如果不等就更新为0. 最后结果取某段max

```text
class Solution:    def findLength(self, A: List[int], B: List[int]) -> int:        n,m = len(A),len(B)        f = [[0]*(m+1) for _ in range(n+1)]        #f[0][0] = 0        res = 0        for i in range(1,n+1):            #f[i][0] = f[i-1][0] + ord(s1[i-1])            for j in range(1,m+1):                #f[0][j] = f[0][j-1] + ord(s2[j-1])                if A[i-1] == B[j-1]:                    f[i][j] = f[i-1][j-1]+1                    res = max(f[i][j],res)        return res
```

