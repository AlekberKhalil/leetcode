# Candy Crush

This question is about implementing a basic elimination algorithm for Candy Crush.

Given a 2D integer array`board`representing the grid of candy, different positive integers`board[i][j]`represent different types of candies. A value of`board[i][j] = 0`represents that the cell at position`(i, j)`is empty. The given board represents the state of the game following the player's move. Now, you need to restore the board to astable stateby crushing candies according to the following rules:

1. If three or more candies of the same type are adjacent vertically or horizontally, "crush" them all at the same time - these positions become empty.
2. After crushing all candies simultaneously, if an empty space on the board has candies on top of itself, then these candies will drop until they hit a candy or bottom at the same time. \(No new candies will drop outside the top boundary.\)
3. After the above steps, there may exist more candies that can be crushed. If so, you need to repeat the above steps.
4. If there does not exist more candies that can be crushed \(ie. the board is

   stable

   \), then return the current board.

You need to perform the above rules until the board becomes stable, then return the current board.

**Example:**

```text
Input:
 board =  [[110,5,112,113,114],[210,211,5,213,214],[310,311,3,313,314],[410,411,412,5,414],[5,1,512,3,3],[610,4,1,613,614],[710,1,2,713,714],[810,1,2,1,1],[1,1,2,2,2],[4,1,4,4,1014]]  
Output:
 [[0,0,0,0,0],[0,0,0,0,0],[0,0,0,0,0],[110,0,0,0,114],[210,0,0,0,214],[310,0,0,113,314],[410,0,0,213,414],[610,211,112,313,614],[710,311,412,613,714],[810,411,512,713,1014]]
```

分析

要同时标记图上所有消零元素，不能改变原图，用set的union \|= 记忆所有元素，最后loop原图一次性消零

标记时候当前数和前面2个比较，3个数取union最大范围

因为同时在原图消零，一直记得判断当前cell是否为零！！！

drop时候注意for i in reversed\(range\(n\)\): \#range\(n-1,-1,-1\) reversed快很多啊

```text
class Solution:
    stable = False
    def candyCrush(self, board: List[List[int]]) -> List[List[int]]:
        if not board or not board[0]:
            return board
        n,m = len(board),len(board[0])
        while True:
            crush = set()
            for i in range(n):
                for j in range(m): 
                    if j > 1 and board[i][j] and board[i][j]==board[i][j-1]==board[i][j-2]: #因为同时在原图消零，一直记得判断当前cell是否为零
                        crush |= {(i,j),(i,j-1),(i,j-2)} #标记时候当前数和前面2个比较，3个数取union最大范围
                    if i > 1 and board[i][j] and board[i][j]==board[i-1][j]==board[i-2][j]:
                        crush |= {(i,j),(i-1,j),(i-2,j)}
            if not crush:
                break

            for i,j in crush: 
                board[i][j] = 0

            for j in range(m):
                idx = n-1
                for i in reversed(range(n)):  #range(n-1,-1,-1)          
                    if board[i][j] :
                        board[idx][j] = board[i][j]
                        idx -= 1
                for x in range(idx+1):
                    board[x][j] = 0
        return board
```

