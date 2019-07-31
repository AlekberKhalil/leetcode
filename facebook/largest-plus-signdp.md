# Largest Plus Sign\(DP\)

In a 2D`grid`from \(0, 0\) to \(N-1, N-1\), every cell contains a`1`, except those cells in the given list`mines`which are`0`. What is the largest axis-aligned plus sign of`1`s contained in the grid? Return the order of the plus sign. If there is none, return 0.

An "axis-aligned plus sign of`1`sof order**k**" has some center`grid[x][y] = 1`along with 4 arms of length`k-1`going up, down, left, and right, and made of`1`s. This is demonstrated in the diagrams below. Note that there could be`0`s or`1`s beyond the arms of the plus sign, only the relevant area of the plus sign is checked for 1s.

**Examples of Axis-Aligned Plus Signs of Order k:**

```text
Order 1:
000
0
1
0
000

Order 2:
00000
00
1
00
0
111
0
00
1
00
00000

Order 3:
0000000
000
1
000
000
1
000
0
11111
0
000
1
000
000
1
000
0000000
```

**Example 1:**

```text
Input:
 N = 5, mines = [[4, 2]]

Output:
 2

Explanation:

11111
11111
1
1
111

111
11
1
1
011
In the above grid, the largest plus sign can only be order 2.  One of them is marked in bold.
```

**Example 2:**

```text
Input:
 N = 2, mines = []

Output:
 1

Explanation:

There is no plus sign of order 2, but there is of order 1.
```

**Example 3:**

```text
Input:
 N = 1, mines = [[0, 0]]

Output:
 0

Explanation:

There is no plus sign, so return 0.
```

**Note:**

```text
N will be an integer in the range [1, 500].
mines will have length at most 5000.
mines[i] will be length 2 and consist of integers in the range [0, N-1].
(Additionally, programs submitted in C, C++, or C# will be judged with a slightly smaller time limit.)
```

分析

dp里存该点开始能延伸到的最大的边长，遇到0就重置为0。4个方向边长都存在这个dp点上，取4个方向里最小的边长。

最后结果就是dp里最大的边长。

1.建一个int\[\]\[\]dp，fill N,在mines里为0，。

2.4个方向尽量延伸得到l,r,u,d，遇到0cell就重置为0。dp都取最小值，这个每个dp里都是存的4个方向里最小的边长。

3.最后整个dp里最大的那个就是最大边长。

```text
class Solution {
    public int orderOfLargestPlusSign(int N, int[][] mines) {
        int[][] dp = new int[N][N];
        for (int i = 0; i < N; i++) {
            Arrays.fill(dp[i], N);
        }
        for(int[] p : mines){
            dp[p[0]][p[1]] = 0;
        }

        for (int i = 0; i < N; i++){
//             for(int j = 0, l = 0; j < N; j ++){
//                 dp[i][j] = Math.min(dp[i][j], l = dp[i][j] == 0 ? 0 : l + 1);
//             }

//             for(int j = N-1, r = 0; j >= 0; j --){
//                 dp[i][j] = Math.min(dp[i][j], r = dp[i][j] == 0 ? 0 : r + 1);
//             }

//             for(int j = 0, u = 0; j < N; j ++){
//                 dp[j][i] = Math.min(dp[j][i], u = dp[j][i] == 0 ? 0 : u + 1);
//             }

//             for(int j = N-1, d = 0; j >= 0; j --){
//                 dp[j][i] = Math.min(dp[j][i], d = dp[j][i] == 0 ? 0 : d + 1);
//             }

            //注意这种简写法。
            for(int j=0,l=0,r=0,u=0,d = 0, k = N-1; j < N; j ++, k --){
                dp[i][j] = Math.min(dp[i][j], l = dp[i][j] == 0 ? 0 : l + 1);

                dp[i][k] = Math.min(dp[i][k], r = dp[i][k] == 0 ? 0 : r + 1);

                dp[j][i] = Math.min(dp[j][i], u = dp[j][i] == 0 ? 0 : u + 1);

                dp[k][i] = Math.min(dp[k][i], d = dp[k][i] == 0 ? 0 : d + 1);
            }

        }

        int o = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0, l = 0; j < N; j++) {
                o = Math.max(dp[i][j],o);
            }
        }
        return o;
    }
}
```

