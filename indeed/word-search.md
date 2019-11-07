# Word Search\(dfs\)

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,  
Given**board**=

```text
[  ['A','B','C','E'],  ['S','F','C','S'],  ['A','D','E','E']]
```

```text
word = "ABCCED", -> returns true,word = "SEE", -> returns true,word = "ABCB", -> returns false.
```

分析

DFS做matrix。这种有重复元素的，visited用二维数组的坐标来判定。

这种有返回值的dfs,遇到合法值直接返回，不用管后来回溯的visite的reset了。

此题找到入口然后开始DFS，四个方向伸展。

```text
class Solution {    static boolean[][] visited;    boolean dfs(char[][] board, int i, int j, String word, int pos){        if(pos == word.length()){            return true;        }        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != word.charAt(pos)  || visited[i][j]){            return false;        }        visited[i][j] = true;        if(dfs(board,i + 1,j, word, pos + 1)            || dfs(board,i,j + 1, word, pos + 1)            || dfs(board,i - 1,j, word, pos + 1)            || dfs(board,i,j - 1, word, pos + 1)){            return true;        }        visited[i][j] = false;        return false;    }    public boolean exist(char[][] board, String word) {        int n = board.length;        int m = board[0].length;         visited = new boolean[n][m];        for(int i = 0; i < n; i ++){            for(int j = 0; j < m; j ++){                                    if((word.charAt(0) == board[i][j]) && dfs(board,i,j, word, 0)){                        return true;                    }                            }        }        return false;    }}
```

