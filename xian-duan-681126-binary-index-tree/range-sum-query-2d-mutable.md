# Range Sum Query 2D - Mutable

Given a 2D matrix, find the sum of the elements inside the rectangle defined by its upper left corner \(row1, col1\) and lower right corner \(row2, col2\). And the elements of the matrix could be changed.

You have to implement three functions:

* `NumMatrix(matrix)`

  The constructor.

* `sumRegion(row1, col1, row2, col2)`

  Return the sum of the elements inside the rectangle defined by its upper left corner \(row1, col1\) and lower right corner \(row2, col2\).

* `update(row, col, val)`

  Update the element at \(row, col\) to

  `val`

  .

## Example

**Example 1:**

```text
Input:
  NumMatrix(
    [[3,0,1,4,2],
     [5,6,3,2,1],
     [1,2,0,1,5],
     [4,1,0,1,7],
     [1,0,3,0,5]]
  )
  sumRegion(2,1,4,3)
  update(3,2,2)
  sumRegion(2,1,4,3)
Output:
  8
  10
```

**Example 2:**

```text
Input:
  NumMatrix([[1]])
  sumRegion(0, 0, 0, 0)
  update(0, 0, -1)
  sumRegion(0, 0, 0, 0)
Output:
  1
  -1
```

## Notice

1. The matrix is only modifiable by

   `update`

   .

2. You may assume the number of calls to update and sumRegion function is distributed evenly.
3. You may assume that row1 ≤ row2 and col1 ≤ col2.

分析

二维数组 binary index tree

注意最后是以x,y为尾的正方形，注意公式

```text
class NumMatrix(object):

    def __init__(self, A):
        """
        :type matrix: List[List[int]]
        """
        if not A or not A[0]:
            return
        self.n, self.m = len(A), len(A[0])
        self.tree = [[0] * (self.m + 1) for _ in range(self.n + 1)]
        self.B = [[0] * (self.m) for _ in range(self.n)]
        for i in range(self.n):

            for j in range(self.m):
                self.update(i, j, A[i][j])


    def update(self, row, col, val):
        """
        :type row: int
        :type col: int
        :type val: int
        :rtype: void
        """
        diff = val - self.B[row][col]
        self.B[row][col] = val

        i = row + 1

        while i <= self.n:
            j = col + 1#每次都要重设
            while j <= self.m:
                self.tree[i][j] += diff
                j += j & (-j)
            i += i & (-i)


    def sumRegion(self, row1, col1, row2, col2):
        """
        :type row1: int
        :type col1: int
        :type row2: int
        :type col2: int
        :rtype: int
        """
        def query(row, col):
            i = row + 1

            sm = 0
            while i > 0:
                j = col + 1
                while j > 0:
                    sm += self.tree[i][j]
                    j -= j & (-j)
                i -= i & (-i)
            return sm

        return query(row2, col2) + query(row1 - 1, col1 - 1) - query(row2, col1 - 1) - query(row1 - 1, col2)




# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# obj.update(row,col,val)
# param_2 = obj.sumRegion(row1,col1,row2,col2)
```

