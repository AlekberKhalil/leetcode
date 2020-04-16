# Sudoku Solver



Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

Empty cells are indicated by the character `'.'`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)  
A sudoku puzzle...

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)  
...and its solution numbers marked in red.

**Note:**

* The given board contain only digits `1-9` and the character `'.'`.
* You may assume that the given Sudoku puzzle will have a single unique solution.
* The given board size is always `9x9`.

分析

dfs或者brute force，就是对于每个格子，loop 1-9尝试放入，然后下一步dfs，可以就返回true，不可以就reset cell

**注意这里先check再放入，为了后面check方便,不污染原matrix**

string.digits去掉0，本身就是char，不需要str\(i\)

2种块坐标表达法

x,y都是到block的初始点，然后+offset 0-3

```text
int row = i - i%3, column = j - j%3;
x,y range(3)
 if(board[row+x][column+y] == val) return false;
 
 i range(9)
 int blkrow = (row / 3) * 3, blkcol = (col / 3) * 3; 
 board[blkrow + i / 3][blkcol + i % 3] == num
```



```text

class Solution:
    def solveSudoku(self, b: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        def check(i,j,c):
            brow = i - i%3 
            bcol = j - j%3
            for x in range(9):
                if b[i][x] == c or b[x][j] == c:
                    return False

            for x in range(3):
                for y in range(3):
                    if b[brow+x][bcol+y] == c:
                        return False
            return True 
        
        def dfs(i,j):
            if i == 9:
                return True
            if j == 9:
                return dfs(i+1,0)
            if b[i][j] !='.':
                return dfs(i,j+1)
            for c in string.digits:
                if c != '0' and check(i,j,c):
                    b[i][j] = c
                    if dfs(i,j+1):
                        return True
                    b[i][j]  = '.'
            return False
        dfs(0,0)
```

