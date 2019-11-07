# N-Queens

Then-queens puzzle is the problem of placingnqueens on ann×nchessboard such that no two queens attack each other.

![](https://leetcode.com/static/images/problemset/8-queens.png)

Given an integern, return all distinct solutions to then-queens puzzle.

Each solution contains a distinct board configuration of then-queens' placement, where`'Q'`and`'.'`both indicate a queen and an empty space respectively.

For example,  
There exist two distinct solutions to the 4-queens puzzle:

```text
[ [".Q..",  // Solution 1  "...Q",  "Q...",  "..Q."], ["..Q.",  // Solution 2  "Q...",  "...Q",  ".Q.."]]
```

分析

这里一个棋盘是一个list&lt;String&gt;，此时col是一个String.解法有N个棋盘放置。所以dfs里每次row到底就是一个棋盘加入ret。

解法主要用到一个list&lt;Integer&gt; cols记录每row的col。这个cols每次加入试探的col index。所以col这个数组不是形如\[1 0 0 1 0\]

而是\[5,3,4,2,1\]。对于每层的row,把每个col的位置都试一遍。

dfs里遍历当前row时col的位置，可以就进入下一个dfs。**判断valid时候此col还未加入cols，**判断时候此时的row也是下一行的，

row=cols.size\(\)

```text
cols.get(i) ==col判断是否在斜线上，看row和col差或者合是否相等，loop此时cols所有行。row = cols.size()，col是此时dfs的试探点。i - cols.get(i) == row - col 左上到右下i + cols.get(i) ==row + col 右上到左下
```

```text
class Solution {    public List<List<String>> solveNQueens(int n) {        List<List<String>> ret = new ArrayList<>();        if(n < 1){            return ret;        }                List<Integer> cols = new ArrayList<Integer>();               dfs(n, cols, ret);          return ret;    }    List<String> draw(int n, List<Integer> cols){        List<String> ret = new ArrayList<String>();               for(int i = 0; i < n ; i ++){            StringBuilder sb = new StringBuilder();                for(int j = 0; j < n ; j ++){                    sb.append(cols.get(i) == j ? "Q" : ".");                }                ret.add(sb.toString());            }          return ret;    }    void dfs(int n, List<Integer> cols, List<List<String>> ret){        if(cols.size() == n){             ret.add(draw(n, cols));                return;        }        for(int i = 0; i < n ; i ++){        //i就是当前col的位置                  if(isValid(i,cols)){                cols.add(i);                dfs(n, cols, ret);                cols.remove(cols.size() - 1);            }        }    }    boolean isValid(int col, List<Integer> cols){        int row = cols.size();        for(int i = 0; i < row;  i ++){           if(cols.get(i) == col || cols.get(i) - i == col - row || cols.get(i) + i == col + row) {               return false;           }                    }        return true;    }}
```

