# Valid Sudoku

Determine if a Sudoku is valid, according to:[Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character`'.'`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.

**Note:**  
A valid Sudoku board \(partially filled\) is not necessarily solvable. Only the filled cells need to be validated.

分析

三个数组row\[i\]\[val\] ，col\[j\]\[val\] ，block\[index\]\[val\] 。此处block的index = i / 3 \* 3 + j / 3

val就是数字1-9，类似dp里背包用val做Index

```text
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if(board == null || board.length == 0 || board[0] == null || board[0].length == 0)
            return false;
        int n = board.length;
        int m = board[0].length;

        int[][] row = new int[n][m];
        int[][]col = new int[n][m];
        int[][] block= new int[n][m];
        for(int i = 0; i < n; i ++){
            for(int j = 0; j < m; j ++){
                if(board[i][j] != '.'){
                    int val = board[i][j] - '0' - 1;
                    int index = i / 3 * 3 + j / 3;
                    if(row[i][val] > 0 || col[j][val] > 0 || block[index][val] > 0){
                        return false;
                    }else{
                        row[i][val] = col[j][val] = block[index][val] = 1;
                    }
                }
            }
        }
        return true;
    }
}
```

用bit做,因为每次loop，row的值都知道了，所以每次loop，row都重设为0，但是col和block的值需要完全loop完整个board才知道，所以用数组存下了col和block所有的值，这里总共81个值。所以数组9

```text
    public boolean isValidSudoku(char[][] board) {
        if(board == null || board.length == 0 || board[0] == null || board[0].length == 0)
            return false;
        int n = board.length;
        int m = board[0].length;
        int row = 0;
        int[] cols = new int[n];
        int[] blocks = new int[n];
        for(int i = 0; i < n; i ++){
            row = 0;//每次loop都能得到row所需所有值，所以每次row都不断更新为0，然后col和block不行，所以需要用数组记录所有值、总共81个值。
            for(int j = 0; j < m; j ++){
                if(board[i][j] != '.'){
                    int cur = board[i][j] - '0';
                int bit = 1 << cur;
                if((row & bit) != 0 || (cols[j] & bit) != 0 || (blocks[(i / 3) * 3 + j / 3] & bit) != 0){
                    return false;
                }
                row |= bit;
                cols[j] |= bit;
                blocks[(i / 3) * 3 + j / 3] |= bit;
                }

            }
        }
        return true;
    }
```

