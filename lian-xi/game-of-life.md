# Game of Life

According to the[Wikipedia's article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life): "The**Game of Life**, also known simply as**Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given aboardwithmbyncells, each cell has an initial statelive\(1\) ordead\(0\). Each cell interacts with its[eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood)\(horizontal, vertical, diagonal\) using the following four rules \(taken from the above Wikipedia article\):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population..
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state \(after one update\) of the board given its current state.

**Follow up**:

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

```text
class Solution {    //用两位表示，所以初始高位总是0，相加时候不改变低位。    public void gameOfLife(int[][] board) {        int n = board.length, m = board[0].length;        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                int cnt = getLiveNeighbors(board, i, j);                if(board[i][j] == 1 && cnt <= 3 && cnt >= 2){                    board[i][j] = 3;                }                 if(board[i][j] == 0 && cnt == 3){                     board[i][j] = 2;                 }            }        }        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                board[i][j] >>= 1;            }        }    }    int getLiveNeighbors(int[][] board, int x, int y){        int n = board.length, m = board[0].length, sum = 0;        //右边界要=        for(int i = Math.max(0, x - 1); i <= Math.min(x + 1, n - 1); i ++){            for(int j = Math.max(0, y - 1); j <= Math.min(y + 1, m - 1); j ++){                sum += board[i][j] & 1;            }        }        sum -= board[x][y] & 1;        return sum;    }}
```

