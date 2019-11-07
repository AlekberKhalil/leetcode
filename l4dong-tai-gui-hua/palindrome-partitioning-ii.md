# Palindrome Partitioning II

Given a strings, partitionssuch that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning ofs.

For example, givens=`"aab"`,  
Return`1`since the palindrome partitioning`["aa","b"]`could be produced using 1 cut.

分析

区间dp

```text
loop // interval :区间从小到大,先枚举区间长度。palindrome partition II
区间的话枚举，start and length
for(int length=2;length<s.length();length++)
    for(int start =0; start+length<s.length();start++)
        isP[start][start+length]=isP[start+1][start+length-1] &&s.charAt(start)==s.charAr(start+length)
```

2个dp,一个dp判断is palidrome,另一个根据结果得到cut。

2个循环i比j多1（不太懂）

cut\[0\]=-1 因为cut\[1\]=0 cut\[1\] = cut\[0\]+1 所以cut\[0\]=-1

2个dp合起来的版本

```text
class Solution {
    public int minCut(String s) {
        int n = s.length();
        int cut[] = new int[n + 1];

        boolean[][] f = new boolean[n][n];
         cut[0] = -1;
        for(int i = 1; i <= n; i ++){ 
            cut[i] = i - 1;
            f[i - 1][i - 1] = true;
            for(int j = 0; j < i; j ++){
                f[j][i - 1] = s.charAt(i - 1) == s.charAt(j) && (i - 1 - j < 2 || f[j + 1][i - 2]) ;
                if(f[j][i - 1]){
                    cut[i] = Math.min(cut[i], cut[j] + 1);
                }
            }
        }

        return cut[n];
    }


}
```

分开dp

```text
class Solution {
    public int minCut(String s) {
        int n = s.length();
        int cut[] = new int[n + 1];
        boolean[][] valid = isPal(s);
         cut[0] = -1;
        for(int i = 1; i <= n; i ++){ 
            cut[i] = i - 1;
            for(int j = 0; j < i; j ++){
                if(valid[j][i - 1]){
                    cut[i] = Math.min(cut[i], cut[j] + 1);//此处j就是i-1
                }
            }
        }

        return cut[n];
    }

    boolean[][] isPal(String s){
        int n = s.length();
        boolean[][] f = new boolean[n][n];
        for(int i = 0; i < n; i ++){
            f[i][i] = true;
            for(int j = 0; j <= i; j ++){               
                    f[j][i] = s.charAt(i) == s.charAt(j) && (i - j < 2 || f[j + 1][i - 1]) ;

            }
        }
        return f;
    }
}
```

网上找的好理解版本。由图可知需要j-1

```text
a   b   a   |   c  c
                j  i
       j-1  |  [j, i] is palindrome
   cut(j-1) +  1
```

```text
public int minCut(String s) {
    char[] c = s.toCharArray();
    int n = c.length;
    int[] cut = new int[n];
    boolean[][] pal = new boolean[n][n];

    for(int i = 0; i < n; i++) {
        int min = i;
        for(int j = 0; j <= i; j++) {
            if(c[j] == c[i] && (j + 1 > i - 1 || pal[j + 1][i - 1])) {
                pal[j][i] = true;  
                min = j == 0 ? 0 : Math.min(min, cut[j - 1] + 1); //#此处要判断j=0的情况 因为有j-1
            }
        }
        cut[i] = min;
    }
    return cut[n - 1];
}
```

