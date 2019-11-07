# Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example**

Given board =

```text
[  "ABCE",  "SFCS",  "ADEE"]
```

word = `"ABCCED"`, -&gt; returns `true`,  
word = `"SEE"`, -&gt; returns `true`,  
word = `"ABCB"`, -&gt; returns `false`.

分析：

DFS，1.要找入口，需要loop矩阵直到找到入口。2这种四个方向需要堵住来路的，可以用board\[x\]\[y\] = '\#';，然后再reset

答案：

```text
public class Solution {    /**     * @param board: A list of lists of character     * @param word: A string     * @return: A boolean     */    int m, n;    char[][] board;     String word;    public boolean exist(char[][] board, String word) {        // write your code here        if(board == null || board[0] == null || word == null)            return false;            n = board.length;            m = board[0].length;            this.board = board;            this.word = word;            boolean ret;            //找到入口            for(int i = 0; i< board.length; i++){                for(int j=0; j< board[0].length; j++){                    if(board[i][j] == word.charAt(0)){                        ret = dfs(i, j, 0);                        if(ret)                            return ret;                    }                }            }            return false;    }    public boolean dfs(int x, int y, int pos){        if(pos == word.length())            return true;        if(x < 0 || x >= n || y < 0 || y >= m || word.charAt(pos) != board[x][y])            return false;        char temp =  board[x][y];        board[x][y] = '#';//标记不可回        //四个方向都可以，所以回路堵住        boolean ret = dfs(x, y+1, pos+1)         || dfs(x+1, y, pos+1)        || dfs(x-1, y, pos+1)        || dfs(x, y-1, pos+1);        board[x][y] = temp;        return ret;    }}
```

