# Maximal Square\(matrix\)

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```text
Input: 1 0 1 0 01 0 1 1 11 1 1 1 11 0 0 1 0Output: 4
```

分析

res\[i\]\[j\] = min\(res\[i - 1\]\[j - 1\], res\[i - 1\]\[j\], res\[i\]\[j - 1\]\) + 1

因为矩阵要i-1,j-1 所以在dp外边框直接加一圈行列都设为0

```text
class Solution:    def maximalSquare(self, matrix):        """        :type matrix: List[List[str]]        :rtype: int        """        if not matrix or not len(matrix):            return 0        n = len(matrix)        m = len(matrix[0])        res = [[0] * (m+1) for _ in range(n+1)]        ans = 0        for i in range(1,n+1):            for j in range(1,m+1):                if int(matrix[i-1][j-1]) == 1:                                        res[i][j] = min(res[i - 1][j - 1], res[i - 1][j], res[i][j - 1]) + 1                ans = max(ans,res[i][j]*res[i][j])        return ans
```

