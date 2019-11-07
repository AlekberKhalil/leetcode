# Range Sum Query 2D - Immutable\(matrix\)

Given a 2D matrixmatrix, find the sum of the elements inside the rectangle defined by its upper left corner \(row1,col1\) and lower right corner \(row2,col2\).

![Range Sum Query 2D](https://leetcode.com/static/images/courses/range_sum_query_2d.png)  
The above rectangle \(with the red border\) is defined by \(row1, col1\) =**\(2, 1\)**and \(row2, col2\) =**\(4, 3\)**, which contains sum =**8**.

**Example:**

```text
Given matrix = [  [3, 0, 1, 4, 2],  [5, 6, 3, 2, 1],  [1, 2, 0, 1, 5],  [4, 1, 0, 1, 7],  [1, 0, 3, 0, 5]]sumRegion(2, 1, 4, 3) -> 8sumRegion(1, 1, 2, 2) -> 11sumRegion(1, 2, 2, 4) -> 12
```

分析

```text
+-----+-+-------+     +--------+-----+     +-----+---------+     +-----+--------+|     | |       |     |        |     |     |     |         |     |     |        ||     | |       |     |        |     |     |     |         |     |     |        |+-----+-+       |     +--------+     |     |     |         |     +-----+        ||     | |       |  =  |              |  +  |     |         |  -  |              |+-----+-+       |     |              |     +-----+         |     |              ||               |     |              |     |               |     |              ||               |     |              |     |               |     |              |+---------------+     +--------------+     +---------------+     +--------------+   sums[i][j]      =    sums[i-1][j]    +     sums[i][j-1]    -   sums[i-1][j-1]   +                          matrix[i-1][j-1]
```

别忘了最后index 是 r2+1 c2+1

```text
class NumMatrix:    def __init__(self, matrix):        """        :type matrix: List[List[int]]        """        if matrix:            n = len(matrix)            m = len(matrix[0])            f = [[0]*(m+1) for _ in range(n+1)]            for i in range(1,n+1):                for j in range(1,m+1):                    f[i][j] = f[i][j-1]+f[i-1][j]-f[i-1][j-1]+matrix[i-1][j-1]            self.f = f        else:            self.f= None    def sumRegion(self, row1, col1, row2, col2):        """        :type row1: int        :type col1: int        :type row2: int        :type col2: int        :rtype: int        """        if not self.f:            return 0        return self.f[row2+1][col2+1]-self.f[row1][col2+1]-self.f[row2+1][col1]+self.f[row1][col1]# Your NumMatrix object will be instantiated and called as such:# obj = NumMatrix(matrix)# param_1 = obj.sumRegion(row1,col1,row2,col2)
```

