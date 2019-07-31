# Knight Dialer

A chess knight can move as indicated in the chess diagram below:

![](https://assets.leetcode.com/uploads/2018/10/12/knight.png) . ![](https://assets.leetcode.com/uploads/2018/10/30/keypad.png)

This time, we place our chess knight on any numbered key of a phone pad \(indicated above\), and the knight makes`N-1`hops. Each hop must be from one key to another numbered key.

Each time it lands on a key \(including the initial placement of the knight\), it presses the number of that key, pressing`N`digits total.

How many distinct numbers can you dial in this manner?

Since the answer may be large,**output the answer modulo`10^9 + 7`**.

* **Example 1:**

```text
Input: 
1
Output: 
10
```

**Example 2:**

```text
Input: 
2
Output: 
20
```

**Example 3:**

```text
Input: 
3
Output: 
46
```

**Note:**

* `1`

  `<`

  `= N`

  `<`

  `= 5000`

分析

python过不了，java

8个方向dfs，记得map里要包含**step**，map\[xtep\]\[x\]\[y\]

```text
class Solution {
    int[][] dd =  {{2,1},{2,-1},{-2,1},{-2,-1},{1,2},{-1,2},{1,-2},{-1,-2}};
    double MOD = Math.pow(10,9) + 7;
    // HashMap<Integer,Integer> mm = new HashMap<>();     

    public int knightDialer(int N) { 
        int res = 0;
        long[][][] mm = new long[N+1][4][3];
        for(int i = 0;i<4;i++){
            for(int j = 0; j<3;j++){               
                    res +=dfs(mm,i,j,N);
                    res%=MOD;              
            }
        }            

        return (int)res;
    }

    public long dfs(long[][][]mm, int x, int y, int step){
        if(x < 0 || y < 0 || x >= 4 || y >= 3 || x== 3 && y!=1) return 0;
         if(mm[step][x][y]>0)
             return mm[step][x][y];
        if (step == 1)
            return 1;
        long res = 0;
        for(int k = 0; k < 8; k ++){           
            int nx = x+dd[k][0];
            int ny = y+dd[k][1];
            // if (0<=nx && nx<4 && 0<=ny && ny<3 && A[nx][ny] != -1)
            res += dfs(mm,nx,ny,step-1);
            res%=MOD;
        }

        mm[step][x][y] = res;
        return res;
    }
}
```

