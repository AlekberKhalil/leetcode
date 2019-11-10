# Valid Tic-Tac-Toe State



A Tic-Tac-Toe board is given as a string array `board`. Return True if and only if it is possible to reach this board position during the course of a valid tic-tac-toe game.

The `board` is a 3 x 3 array, and consists of characters `" "`, `"X"`, and `"O"`.  The " " character represents an empty square.

Here are the rules of Tic-Tac-Toe:

* Players take turns placing characters into empty squares \(" "\).
* The first player always places "X" characters, while the second player always places "O" characters.
* "X" and "O" characters are always placed into empty squares, never filled ones.
* The game ends when there are 3 of the same \(non-empty\) character filling any row, column, or diagonal.
* The game also ends if all squares are non-empty.
* No more moves can be played if the game is over.

```text
Example 1:
Input: board = ["O  ", "   ", "   "]
Output: false
Explanation: The first player always plays "X".

Example 2:
Input: board = ["XOX", " X ", "   "]
Output: false
Explanation: Players take turns making moves.

Example 3:
Input: board = ["XXX", "   ", "OOO"]
Output: false

Example 4:
Input: board = ["XOX", "O O", "XOX"]
Output: true
```

分析

h,v,l,r用Counter,可以用来存对角线 x-y 不用担心负数

存储4个方向累积数字和turn，Player1 ++Player -- 。最后比较是 == +n 还是-n

最后可能不合法结果

1 turn1 和win 0 或者win1 和turn 0

2 都win。 

3 turn只能0,1

```text
from collections import Counter
class Solution:
    def validTicTacToe(self, board: List[str]) -> bool:
        h, v, l, r = Counter(), Counter(), Counter(), Counter()
        turn = 0
        for i in range(3):
            for j in range(3):
                if board[i][j] == 'X' :
                    turn += 1
                    h[i] += 1
                    v[j] += 1
                    l[i + j] += 1
                    r[i - j] += 1
                elif board[i][j] == 'O':
                    turn -= 1
                    h[i] -= 1
                    v[j] -= 1
                    l[i + j] -= 1
                    r[i - j] -= 1
        xwin = owin = False           
        for i in range(3):
            for j in range(3):
                xwin |= h[i] == 3 or v[j] == 3 or l[i+j] == 3 or r[i-j] == 3
                owin |= h[i] == -3 or v[j] == -3 or l[i+j] == -3 or r[i-j] == -3
        
        
        if xwin and turn == 0 or owin and turn == 1 or turn not in {0,1} or xwin and owin:
            return False
        return True

        
```



