# Edit Distance

Given two wordsword1andword2, find the minimum number of steps required to convertword1toword2. \(each operation is counted as 1 step.\)

You have the following 3 operations permitted on a word:

a\) Insert a character  
b\) Delete a character  
c\) Replace a character  
分析

长度不足1的时候不能进入循环，所以初始化还是放外面。

c的情况是f\[i - 1\]\[j - 1\] + 1

```text
class Solution {
    public int minDistance(String word1, String word2) {
        int n = word1.length();
        int m = word2.length();
        int[][] f = new int[n + 1][m + 1];
        //不能在循环里初始化，是为了防止a,b的长度不足1时候。
        for(int i=0; i< m+1; i++){
            f[0][i] = i; 
        }
        for(int i=0; i<n+1; i++){
            f[i][0] = i;
        }
        for(int i = 1; i <= n; i ++){            
            for(int j = 1; j <= m; j ++){  
                if(word1.charAt(i-1) == word2.charAt(j-1)){
                    f[i][j] = f[i - 1][j - 1];
                }else{
                    f[i][j] = Math.min(f[i - 1][j - 1], Math.min(f[i-1][j],f[i][j-1])) + 1;
                }
                //loop里也可以
                 //f[i][j] = word1.charAt(i-1) == word2.charAt(j-1) ? f[i - 1][j - 1] : f[i - 1][j - 1] + 1;                
                 //f[i][j] = Math.min(f[i][j], Math.min(f[i-1][j],f[i][j-1]) + 1);

            }
        }
        return f[n][m];
    }
}
```

