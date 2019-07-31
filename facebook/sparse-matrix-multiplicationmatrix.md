# Sparse Matrix Multiplication\(matrix\)

Given two[Sparse Matrix](https://en.wikipedia.org/wiki/Sparse_matrix)A and B, return the result of AB.

You may assume that A's column number is equal to B's row number.

## Example

```text
A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]

B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]


     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
```

分析

RowA i \* ColB j = ret\[i,j\] 找到ret的坐标即可

```text
class Solution:
    """
    @param A: a sparse matrix
    @param B: a sparse matrix
    @return: the result of A * B
    """
    def multiply(self, A, B):
        # write your code here
        rowA = len(A)
        colA = len(A[0]) 
        colB = len(B[0])
        ret = [[0]*colB for _ in range(rowA)]
        for rowa in range(rowA):
            for colb in range(colB):
                cellsum = 0
                for cell in range(colA):
                    cellsum += A[rowa][cell]*B[cell][colb]
                ret[rowa][colb] = cellsum

        return ret
```

