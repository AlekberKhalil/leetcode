# Distinct subsequences

Given a string**S**and a string**T**, count the number of distinct subsequences of**S**which equals**T**.

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie,`"ACE"`is a subsequence of`"ABCDE"`while`"AEC"`is not\).

Here is an example:  
**S**=`"rabbbit"`,**T**=`"rabbit"`

Return`3`.

分析

s里可以删也可以取（相等时候），就像unique path一样，几种来到当前点的路径相加。

```text
 * Path[i][j] = Path[i][j-1]            (discard S[j])
 *              +     Path[i-1][j-1]    (S[j] == T[i] and we are going to use S[j])
 *                 or 0                 (S[j] != T[i] so we could not use S[j])
 * while Path[0][j] = 1 and Path[i][0] = 0.//初始化
```

```text
class Solution {
    public int numDistinct(String s, String t) {
        int n = s.length();
        int m = t.length();
        if(m > n) return 0;
        int[][] f = new int[n + 1][m + 1];
        //不能在循环里初始化，是为了防止a,b的长度不足1时候。

        for(int i=0; i< n+1; i++){
            f[i][0] = 1; #对角线上的 需要给1开始。也可以是S全部删掉，至少有1种。
        }#不要初始f[0][j]因为后面无论如何f[i][j] = f[i-1][j]，该是0

        for(int i = 1; i <= n; i ++){            
            for(int j = 1; j <= m; j ++){                 
                    f[i][j] = f[i - 1][j] + (s.charAt(i-1) == t.charAt(j-1) ? f[i - 1][j - 1] : 0);                                             
            }
        }
        return f[n][m];
    }
}
```

