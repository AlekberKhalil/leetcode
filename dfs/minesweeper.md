# Minesweeper

```text
Let's play the minesweeper game (Wikipedia, online game)!You are given a 2D char matrix representing the game board. 'M' represents an unrevealed mine, 'E' represents an unrevealed empty square, 'B' represents a revealed blank square that has no adjacent (above, below, left, right, and all 4 diagonals) mines, digit ('1' to '8') represents how many mines are adjacent to this revealed square, and finally 'X' represents a revealed mine.Now given the next click position (row and column indices) among all the unrevealed squares ('M' or 'E'), return the board after revealing this position according to the following rules:If a mine ('M') is revealed, then the game is over - change it to 'X'.If an empty square ('E') with no adjacent mines is revealed, then change it to revealed blank ('B') and all of its adjacent unrevealed squares should be revealed recursively.If an empty square ('E') with at least one adjacent mine is revealed, then change it to a digit ('1' to '8') representing the number of adjacent mines.Return the board when no more squares will be revealed.Example 1:Input: [['E', 'E', 'E', 'E', 'E'], ['E', 'E', 'M', 'E', 'E'], ['E', 'E', 'E', 'E', 'E'], ['E', 'E', 'E', 'E', 'E']]Click : [3,0]Output: [['B', '1', 'E', '1', 'B'], ['B', '1', 'M', '1', 'B'], ['B', '1', '1', '1', 'B'], ['B', 'B', 'B', 'B', 'B']]Explanation:Example 2:Input: [['B', '1', 'E', '1', 'B'], ['B', '1', 'M', '1', 'B'], ['B', '1', '1', '1', 'B'], ['B', 'B', 'B', 'B', 'B']]Click : [1,2]Output: [['B', '1', 'E', '1', 'B'], ['B', '1', 'X', '1', 'B'], ['B', '1', '1', '1', 'B'], ['B', 'B', 'B', 'B', 'B']]Explanation:Note:The range of the input matrix's height and width is [1,50].The click position will only be an unrevealed square ('M' or 'E'), which also means the input board contains at least one clickable square.The input board won't be a stage when game is over (some mines have been revealed).For simplicity, not mentioned rules should be ignored in this problem. For example, you don't need to reveal all the unrevealed mines when the game is over, consider any cases that you will win the game or flag any squares.
```

分析

空点进行DFS，8个方向得到雷数然后决定1该点设数字停，2设B继续DFS

记住设置完当前x,y以后再dfs8个方向。否则爆栈

```text
class Solution:    def updateBoard(self, A: List[List[str]], click: List[int]) -> List[List[str]]:        if not A or not A[0]:            return A        d = [-1, 0, 1, 0, -1]        n, m = len(A), len(A[0])        x,y =click[0],click[1]        if A[x][y] == 'M':            A[x][y]='X'            return A        def dfs(x,y):                            if A[x][y]=='E':                  minecnt = 0                for nx, ny in [(x-1,y),(x+1,y),(x,y+1),(x,y-1),(x-1,y-1),(x+1,y+1),(x-1,y+1),(x+1,y-1)]:                    if 0 <= nx < n and 0 <= ny < m and A[nx][ny] == 'M' :                            minecnt += 1                                      if minecnt:                     A[x][y]=str(minecnt)                     return                else:                    A[x][y]='B'                for nx, ny in [(x-1,y),(x+1,y),(x,y+1),(x,y-1),(x-1,y-1),(x+1,y+1),(x-1,y+1),(x+1,y-1)]:                    if 0 <= nx < n and 0 <= ny < m :                        dfs(nx,ny)        dfs(x,y)        return A
```

网上DFS简易写法

```text
def updateBoard(self, board, click):    (row, col), directions = click, ((-1, 0), (1, 0), (0, 1), (0, -1), (-1, 1), (-1, -1), (1, 1), (1, -1))    if 0 <= row < len(board) and 0 <= col < len(board[0]):        if board[row][col] == 'M':            board[row][col] = 'X'        elif board[row][col] == 'E':            n = sum([board[row + r][col + c] == 'M' for r, c in directions if 0 <= row + r < len(board) and 0 <= col + c < len(board[0])])            board[row][col] = str(n or 'B')            for r, c in directions * (not n): self.updateBoard(board, [row + r, col + c])    return board
```

